# captive-browser

A more secure, dedicated, Chrome-based captive portal browser that automatically bypasses custom DNS servers.

`captive-browser` detects the DHCP DNS server and runs a SOCKS5 proxy that resolves hostnames through it. Then it starts a Chrome instance in Incognito mode with a separate data directory and waits for it to exit.

[Read more on my blog.](https://blog.filippo.io/captive-browser)

## Installation

You'll need Chrome and Go 1.9 or newer.

```
go get -u github.com/FiloSottile/captive-browser
```

You have to install a config file in `$XDG_CONFIG_HOME/captive-browser.toml` (if set) or `~/.config/captive-browser.toml`. You can probably use one of the stock ones below. You might have to modify the network interface.

### macOS

```
cp $(go env GOPATH)/src/github.com/FiloSottile/captive-browser/captive-browser-mac-chrome.toml ~/.config/captive-browser.toml
```

To disable the insecure system captive browser [see here](https://github.com/drduh/macOS-Security-and-Privacy-Guide#captive-portal). If that doesn't work, disable SIP (remember to re-enable it), and rename `/System/Library/CoreServices/Captive Network Assistant.app`.

### Linux

#### Ubuntu

```
cp $(go env GOPATH)/src/github.com/FiloSottile/captive-browser/captive-browser-ubuntu-chrome.toml ~/.config/captive-browser.toml
```

#### Arch / systemd-networkd

```
go get -u github.com/FiloSottile/captive-browser/cmd/systemd-networkd-dns
cp $(go env GOPATH)/src/github.com/FiloSottile/captive-browser/captive-browser-arch-chrome.toml ~/.config/captive-browser.toml
```

#### Arch / dhcpcd

```
cp $(go env GOPATH)/src/github.com/FiloSottile/captive-browser/captive-browser-dhcpcd-chromium.toml ~/.config/captive-browser.toml
```

#### Flatpak

```
cp $(go env GOPATH)/src/github.com/FiloSottile/captive-browser/captive-browser-flatpak-chromium.toml ~/.config/captive-browser.toml
```

## Usage

Simply run `captive-browser`, log into the captive portal, and then *quit* (⌘Q / Ctrl-Q) the Chrome instance.

If the binary is not found, try `$(go env GOPATH)/bin/captive-browser`.

To configure the browser, open a non-Incognito window (⌘N / Ctrl-N).
