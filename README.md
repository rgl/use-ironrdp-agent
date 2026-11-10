# About

Shows how to use the [ironrdp-agent](https://github.com/Devolutions/IronRDP/tree/master/crates/ironrdp-agent) to control a Windows machine via the Remote Desktop Protocol (RDP).

## Usage

```bash
#wget -O- https://github.com/Devolutions/IronRDP/releases/download/ironrdp-agent-v0.1.0/ironrdp-agent-0.1.0-linux-x64.tar.gz | tar xzf - -C "$PWD"
#alias ironrdp-agent="$PWD/ironrdp-agent"
cargo install --git https://github.com/Devolutions/IronRDP.git --rev cc63ef7d6477fc20b7667bb7e2bd4775c1f55145 ironrdp-agent
ironrdp-agent --help
ironrdp-agent --help-agent
ironrdp-agent \
    daemon-start \
    --skip-certificate-check \
    &
# export AGENT_RDP_USERNAME=Administrator
# export AGENT_RDP_PASSWORD=vagrant
ironrdp-agent \
    connect \
    --server 192.168.8.22 \
    --username Administrator \
    --password vagrant \
    --prop desktopwidth:i:1280 \
    --prop desktopheight:i:720
ironrdp-agent \
    status
ironrdp-agent \
    query-props
ironrdp-agent \
    query-logs
ironrdp-agent \
    mouse-move \
    --x 38 \
    --y 690
ironrdp-agent \
    mouse-button \
    --button left \
    --pressed true
ironrdp-agent \
    mouse-button \
    --button left \
    --pressed false
ironrdp-agent \
    screenshot \
    desktop.png
xdg-open desktop.png
# NB you must install the Devolutions Agent inside the RDP server machine. e.g., using the powershell script:
#       $archiveUrl = 'https://github.com/Devolutions/devolutions-gateway/releases/download/v2026.3.3/DevolutionsAgent-2026.3.3-x64.msi'
#       $archivePath = "$env:TEMP\$(Split-Path -Leaf $archiveUrl)"
#       (New-Object System.Net.WebClient).DownloadFile($archiveUrl, $archivePath)
#       $logPath = "$archivePath.install.log"
#       # NB this installs the binaries to C:\Program Files\Devolutions\Agent.
#       # NB this installs and starts the DevolutionsAgent service (runs-as SYSTEM).
#       msiexec /i $archivePath /qn /L*v "$archivePath.log" | Out-String -Stream
#       if ($LASTEXITCODE) {
#           throw "installation failed with exit code $LASTEXITCODE (0x$($LASTEXITCODE.ToString('X8'))). See $archivePath.log."
#       }
# see https://github.com/Devolutions/IronRDP/issues/1889
ironrdp-agent \
    now \
    capabilities
ironrdp-agent \
    now \
    exec \
    process \
    whoami.exe \
    --parameters '/all'
ironrdp-agent \
    now \
    pwsh \
    'whoami /all'
ironrdp-agent \
    now \
    pwsh \
    '$PSVersionTable'
ironrdp-agent \
    now \
    powershell \
    '$PSVersionTable'
ironrdp-agent \
    now \
    exec \
    process \
    query.exe \
    --parameters 'user'
# logoff.
# NB there's no ironrdp-agent disconnect --logoff or logoff command, so
#    workaround by executing logoff.exe.
#    see https://github.com/Devolutions/IronRDP/issues/1855
ironrdp-agent \
    now \
    exec \
    process \
    logoff.exe
# or disconnect.
ironrdp-agent \
    disconnect
ironrdp-agent \
    status
```

## Alternatives

* https://github.com/FlaUI/FlaUI
* https://github.com/floatingbrij/desktop-pilot-mcp
* https://github.com/sh3ll3x3c/native-devtools-mcp
* https://github.com/thisnick/agent-rdp

## References

* https://github.com/Devolutions/IronRDP
