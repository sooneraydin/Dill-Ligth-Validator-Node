# Dill-Ligth-Validator-Node
![image](https://github.com/user-attachments/assets/94e0ba96-7db4-44db-88b3-577651358207)


## 💻 Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler |
| Ubuntu 22.04|
| 2 GB Memory, 2 vCPUs Processing, 60 GB SSD Storage, 3 TB Transfer|

### 🚧Kullanılan Portlar
| 8080 : 3500 : 4000 : 8082 : 13000 : 8551 : 8545 : 30303 | 

### 🚧Gerekli kurulumlar
```
sudo apt-get update && sudo apt-get upgrade -y
```

### Dosyaları çekiyoruz sunucumuza
```
curl -O https://dill-release.s3.ap-southeast-1.amazonaws.com/linux/dill.tar.gz
```

```
tar -xzvf dill.tar.gz && cd dill
```

### Validatörümüzü oluşturuyoruz.
```
./dill_validators_gen new-mnemonic --num_validators=1 --chain=andes --folder=./
```

 ### Çıktı Bu şekilde olmalı
- ubuntu@ip-xxxx:~/dill$ ./dill_validators_gen new-mnemonic --num_validators=1 --chain=andes --folder=./
- ***Using the tool on an offline and secure device is highly recommended to keep your mnemonic safe.***
- Please choose your language ['1. العربية', '2. ελληνικά', '3. English', '4. Français', '5. Bahasa melayu', '6. Italiano', '7. 日本語', '8. 한국어', '9. Português do Brasil', '10. român', '11. Türkçe', '12. 简体中文']:  [English]: 3
- Please choose the language of the mnemonic word list ['1. 简体中文', '2. 繁體中文', '3. čeština', '4. English', '5. Italiano', '6. 한국어', '7. Português', '8. Español']:  [english]: 4
- Create a password that secures your validator keystore(s). You will need to re-enter this to decrypt them when you setup your Dill validators.:
- Repeat your keystore password for confirmation:
- The amount of DILL token to be deposited(2500 by default). [2500]:
- This is your mnemonic (seed phrase). Write it down and store it safely. It is the ONLY way to retrieve your deposit.
- Creating your keys.
- Creating your keystores:	  [####################################]  1/1
- Verifying your keystores:	  [####################################]  1/1
- Verifying your deposits:	  [####################################]  1/1
- Success!
- Your keys can be found at: ./validator_keys
- Press any key.
- ubuntu@ip-xxxx:~/dill$


### Validatör key oluşturyoruz
```
./validator_keys
```
### Çıktı Bu şekilde olmalı
- ubuntu@ip-xxxxx:~/dill$ ls -ltr ./validator_keys
- total 8
- -r--r----- 1 ubuntu ubuntu 710 Jul 13 08:06 keystore-m_12381_3600_0_0_0-xxxxxx.json
- -r--r----- 1 ubuntu ubuntu 706 Jul 13 08:06 deposit_data-xxxx.json

### Anahtarlarınızı anahtar deponuza aktarıoruz
```
./dill-node accounts import --andes --wallet-dir ./keystore --keys-dir validator_keys/ --accept-terms-of-use
```
### Çıktı Bu şekilde olmalı
- [2024-07-13 08:08:34]  INFO flags: Running on the Andes Beacon Chain Testnet
- Password requirements: at least 8 characters
- New wallet password:
- Confirm password:
- [2024-07-13 08:08:39]  INFO wallet: Successfully created new wallet walletPath=/home/ubuntu/dill/keystore
- [2024-07-13 08:08:39]  WARN client: You are using an insecure gRPC connection. If you are running your beacon node and validator on the same machines, you can ignore this message. If you want to know how to enable secure connections, see: - https://docs.prylabs.network/docs/prysm-usage/secure-grpc
- [2024-07-13 08:08:39]  INFO accounts: importing validator keystores...
- [2024-07-13 08:08:39]  INFO accounts: checking directory for keystores: /home/ubuntu/dill/validator_keys
- Enter the password for your imported accounts:
- Importing accounts, this may take a while...
- Importing accounts... 100% [===================================================================================]  [1s:0s]
- [2024-07-13 08:08:44]  INFO local-keymanager: Reloaded validator keys into keymanager
- [2024-07-13 08:08:44]  INFO local-keymanager: Successfully imported validator key(s) pubkeys=0xxxxx
- [2024-07-13 08:08:44]  INFO accounts: Imported accounts [xxxxxx], view all of them by running `accounts list`

  ### Parolamızı oluşturyoruz (ben hep aynı şifreyi kullandım) {my-password} olan yeri parantezleride silinecek şekilde değiştirin
  ```
  echo {my-password} > walletPw.txt
  ```

  ### Ve Nodumuzu Çalıştırıyoruz (<password-path> olan yere şifremizi yazıyoruz)
  ```
  ./start_light.sh -p <password-path>
  ```

  ### Çıktı Bu şekilde olmalı
  - Option --pwdfile, argument 'walletPw.txt'
  - Remaining arguments:
  - using password file at walletPw.txt
  - start light node
  - start light node done

  ### Ve Nodumuzu Kontrol ediyoruz
  ```
  ps -ef | grep dill
  ```

  ### Çıktı Bu şekilde olmalı
  - ubuntu      1981       1 86 08:09 pts/0    00:00:43 /home/ubuntu/dill/dill-node --light --embedded-geth --datadir /home/ubuntu/dill/light_node/data/beacondata --genesis-state /home/ubuntu/dill/genesis.ssz --grpc-gateway-host 0.0.0.0 --initial-validators /home/ubuntu/dill/validators.j
 
  ### STAKE EDECEĞİZ Platformdan yapacağız
  - deposit_data-*.json dosyasını sunucumuzdan indirmemiz lazım
  - dill dosyası içindeki  .validatör_keys dosyası içerisinde
  - kopyalama işlemini yaptıktan sonra siteye bağlanarak dosyamızı buraya ekleyerek validatörmüze bağlanıyoruz.
  - https://staking.dill.xyz/
    
  ![image](https://github.com/user-attachments/assets/ede3c2bf-8687-413d-a766-ed33cf76a41a)

  - bu işlemi yaptıktan sonra diğer sayfaya geçiyoruz.
  - discorddan faucet istiyoruz. Faucet geldikten sonra stake işlemini gerçekleştiriyoruz.
  ![image](https://past-chokeberry-e85.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa156a5a1-885f-491c-90e5-49580a8f7a9b%2Ff767e031-4ef1-4374-91e1-bd9cbc58e769%2FUntitled.png?table=block&id=cfefaea7-8df1-47a9-8537-2e01dba0fff5&spaceId=a156a5a1-885f-491c-90e5-49580a8f7a9b&width=2000&userId=&cache=v2)

- En son bu şekilde olması gerekiyor.
  ![image](https://past-chokeberry-e85.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa156a5a1-885f-491c-90e5-49580a8f7a9b%2F007ad42b-cccd-46a8-9129-f848a0e5877b%2FUntitled.png?table=block&id=a2b12bfe-0766-4932-816b-fbea2ea65ef9&spaceId=a156a5a1-885f-491c-90e5-49580a8f7a9b&width=1420&userId=&cache=v2)



testtt


