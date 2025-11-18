# Create `postgres` group / user in Linux

```
groupadd -g 41 postgres
```

```
useradd -c "PostgreSQL Server" -g postgres -d /opt/pgsql/data  -u 41 postgres
```
# Change Listening Address / Port in `postgresql.conf`

```
sudo nano /etc/postgresql/17/main/postgresql.conf
```

```
	listen_addresses = '*'
	port = 5432
```

# Change `PosgreSQL` Host Based Authentication File

```
sudo nano /etc/postgresql/17/main/pg_hba.conf
```
## CIDR Mask: 

```
host    all    all    192.168.1.0/24    scram-sha-256
```
or allow only one host:  

```
 host all all 192.168.1.50/32 md5
```

```
sudo systemctl restart postgresql
```
```
ss -tulpen | grep 5432
```

## Change PostgreSQL Password
```
sudo -u postgres psql -c "ALTER USER postgres PASSWORD '123';"
```
or 
```
postgres=# \password postgres
Enter new password: <new-password>
postgres=# \q

```


# Create PostgreSQL Server / Application Certs

### 1.Create Root Certificate:

```
openssl genrsa -out rootCA.key 4096
```

```
openssl req -x509 -new -nodes -key rootCA.key  -sha256 -days 3650   -subj "/CN=PostgresRootCA"   -out rootCA.crt
```
### 2.Create Server certificate signed by the CA

```
openssl genrsa -out server.key 2048

```

```
chmod 600 server.key
```

```
openssl req -new  -key server.key  -subj "/CN=192.168.1.20"  -out server.csr
```

```
openssl x509 -req  -in server.csr  -CA rootCA.crt  -CAkey rootCA.key -CAcreateserial  -days 3650 -sha256  -out server.crt
```
### 3.Generate Client Certificate for Application
```
openssl genrsa -out app.key 2048
```

```
chmod 600 app.key
```

CN should be the name of your Database:
```
openssl req  -new  -key app.key  -subj "/CN=postgres"  -out app.csr
```

```
openssl x509 -req -in app.csr   -CA rootCA.crt   -CAkey rootCA.key   -CAcreateserial   -days 3650 -sha256   -out app.crt
```

# Configure PostgreSQL to Accept  Client's  Certificate

### 1. Update `postgresql.conf` file:

```
ssl = on
ssl_cert_file = 'server.crt'
ssl_key_file  = 'server.key'
ssl_ca_file   = 'rootCA.crt'
```

```
chmod 600 server.key
```
### 2. Update `pg_hba.conf` file:

```
hostssl all all 0.0.0.0/0 cert clientcert=verify-full
```
Or restrict to specific role:
```
hostssl mydb myuser 203.0.113.45/32 cert clientcert=verify-full
```

### 3.Connect to PostgreSQL Server from Client
```
psql "host=db.example.com port=5432 dbname=mydb user=postgres sslmode=verify-full  sslrootcert=rootCA.crt   sslcert=app.crt sslkey=app.key"
```


### *.PEM and *.CER are base64 and *.DER is binary
