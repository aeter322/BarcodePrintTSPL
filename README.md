# BarcodePrintTSPL
 The repository is created for printing on a thermal printer in Unix-like systems using the TSPL protocol, in particular for printing labels with barcodes
## install
```bash
git clone https://github.com/aeter322/BarcodePrintTSPL
cd BarcodePrintTSPL
sudo pip3 install -r requirements.txt
sudo python3 setup.py install

## set up configuration

sudo mkdir /etc/barcode_service
sudo cp configs.ini.example /etc/barcode_service/config.ini

## set up systemd-service

sudo cp scripts/barcode.service /lib/system/
sudo systemctl daemon-reload
sudo systemctl enable barcode.service

## start service

sudo systemctl start barcode.service
