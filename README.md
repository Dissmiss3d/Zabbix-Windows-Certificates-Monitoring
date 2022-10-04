# Zabbix-Windows-Certificates-Monitoring

Agent dosyası içerisinde "scripts" klasörü oluşturarak ps doyalarını içeri atıyoruz.

Agent.conf içerisine aşağıdaki gibi userparameter ekliyoruz;

UserParameter=windows.certs[*],powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Program Files\zabbix-agent\scripts\windows_certs.ps1" -ActionType "$1" -Key "$2" -Value "$3"
Templatei assing ettiğimizde otomatik discovery ederek item-triggerları oluşturuyor.


Zabbix v5.0.10 ve Agent v5 test edildi.
