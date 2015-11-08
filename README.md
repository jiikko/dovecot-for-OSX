# dovecot-for-OSX
自動テスト環境で使うimap/popサーバをインストールする手順です。
static で認証します。

* dovecot 2.2.18

## Installation bin/dovecot
```
brew install dovecot
```
### start & stop
```
sudo launchctl stop homebrew.mxcl.dovecot
sudo launchctl start homebrew.mxcl.dovecot
```

## Setup config
### replace gid & uid

```
vi config/conf.d/auth-static.conf.ext
```

## copy config
```
cp ./config/* /usr/local/etc/dovecot/
cp ./config/conf.d/* /usr/local/etc/dovecot/conf.d/
```

## Testing
```
require 'net/imap'
imap = Net::IMAP.new(HOST, { port: 143 })
imap.authenticate('localhost', "koji", "test")
imap.logout
```
