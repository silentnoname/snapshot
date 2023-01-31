Update Time **2023-01-31 12:40 UTC**    
```
cd $HOME
sudo apt install snap -y
snap install lz4
sudo systemctl stop okp4d
cp $HOME/.okp4d/data/priv_validator_state.json $HOME/.okp4d/priv_validator_state.json.backup
wget -O okp4.tar.lz4 http://snapshot.silentvalidator.com/testnet/okp4/okp4-2023-01-31T12%3A40.tar.lz4 --inet4-only
okp4d tendermint unsafe-reset-all --home $HOME/.okp4d --keep-addr-book
lz4 -c -d okp4.tar.lz4  | tar -x -C $HOME/.okp4d
mv $HOME/.okp4d/priv_validator_state.json.backup $HOME/.okp4d/data/priv_validator_state.json
sudo systemctl restart okp4d && journalctl -u okp4d -f -o cat
```
You can delete the file to save disk
```
rm okp4.tar.lz4 
```