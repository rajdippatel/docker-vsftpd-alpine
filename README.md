# docker-vsftpd-alpine
vsftpd Docker image build script based on Alpine

Supports passive mode and virtual users.

## How to run

Use `docker-compose`

**Modify `docker-compose.yml` to fit you need.**

```
git clone https://github.com/epoweripione/docker-vsftpd-alpine.git
cd docker-vsftpd-alpine
docker-compose up -d
```

## Something to do
`docker exec -i -t vsftpd_vsftpd_1 sh`

1. Set `admin` password

```
echo "admin:$(openssl passwd -1 AdminPWD)" >> /etc/vsftpd/virtual_users
cat > /etc/vsftpd/vsftpd_user_conf/admin <<EOF
anon_world_readable_only=NO
write_enable=YES
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_other_write_enable=YES
local_root=/home/ftp/
EOF
```

2. Add Virtual FTP User

Replace `myuser` and `mypass` to what you want `<user name>` and `<user password>`.

User's root path, upload and write permission in file /etc/vsftpd/vsftpd_user_conf/`<username>`, you can change them for security reason.

```
mkdir -p /home/ftp/myuser
echo "myuser:$(openssl passwd -1 mypass)" >> /etc/vsftpd/virtual_users
cat > /etc/vsftpd/vsftpd_user_conf/myuser <<EOF
anon_world_readable_only=NO
write_enable=YES
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_other_write_enable=YES
local_root=/home/ftp/myuser
EOF
```
