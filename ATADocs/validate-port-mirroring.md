---
title: Validação do espelhamento de porta no Advanced Threat Analytics | Microsoft Docs
description: Descreve como validar que o espelhamento de porta está configurado corretamente
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8ebc7598128abe1fbebd10418bada5d68d9df9a1
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="validate-port-mirroring"></a>Validação do espelhamento de porta
> [!NOTE] 
> Este artigo somente é relevante se você implanta Gateways do ATA em vez de Gateways Lightweight do ATA. Para determinar se você precisa usar Gateways do ATA, confira [Choosing the right gateways for your deployment](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment) (Escolhendo os gateways certos para sua implantação).
 
As etapas a seguir guiarão você pelo processo de validação da configuração correta do espelhamento de porta. Para que o ATA funcione corretamente, o Gateway de ATA deve ser capaz de ver o tráfego para e do controlador de domínio. A fonte de dados principal usada pelo ATA é uma inspeção profunda de pacotes do tráfego de rede para e dos controladores de domínio. Para o ATA ver o tráfego de rede, o espelhamento de porta precisa ser configurado. O espelhamento de porta copia o tráfego de uma porta (de origem) para outra porta (de destino).

## <a name="validate-port-mirroring-using-a-windows-powershell-script"></a>Validar espelhamento de porta usando um script do Windows PowerShell

1. Salve o texto do script em um arquivo chamado *ATAdiag.ps1*.
2. Execute esse script no Gateway do ATA que você deseja validar.
O script gera o tráfego ICMP do Gateway do ATA para o controlador de domínio e procura esse tráfego no NIC de Captura no controlador de domínio.
Se o Gateway do ATA vê o tráfego ICMP com um endereço IP de destino igual ao endereço IP do DC que você digitou no Console do ATA, ele considera o espelhamento de porta configurado. 

Exemplo de como executar o script:

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## <a name="validate-port-mirroring-using-net-mon"></a>Validar o espelhamento de porta usando Net Mon
1.  Instale o [Monitor de Rede da Microsoft 3.4](http://www.microsoft.com/download/details.aspx?id=4865) no Gateway do ATA que você deseja validar.

    > [!IMPORTANT]
    > Não instale o Microsoft Message Analyzer ou qualquer outro software de captura de tráfego no Gateway de ATA.

2.  Abra o Monitor de Rede e crie uma nova guia de captura.

    1.  Selecione apenas o adaptador de rede de **captura** ou o adaptador de rede que estiver conectado à porta do comutador configurado como o destino do espelhamento de porta.

    2.  Verifique se o Modo-P está habilitado.

    3.  Clique em **Nova captura**.

        ![Criar nova imagem da guia de captura](media/ATA-Port-Mirroring-Capture.jpg)

3.  Na janela Filtro de exibição, digite o seguinte filtro: **KerberosV5 OU LDAP** e, em seguida, **Aplicar**.

    ![Aplicar imagem de filtro KerberosV5 ou LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Clique em **Iniciar** para iniciar a sessão de captura. Se você não vir o tráfego para e do controlador de domínio, examine a configuração do espelhamento de porta.

    ![Iniciar a captura de imagem de sessão](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > É importante ter certeza de que você vê o tráfego para e dos controladores de domínio.
    

5.  Se você vir somente o tráfego em uma direção, você deve trabalhar com as equipes de rede ou de virtualização para ajudar a solucionar os problemas de sua configuração de espelhamento de porta.

## <a name="see-also"></a>Consulte Também

- [Configurar o espelhamento de porta](configure-port-mirroring.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
