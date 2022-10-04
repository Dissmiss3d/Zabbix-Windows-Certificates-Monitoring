# Zabbix-Windows-Certificates-Monitoring

Agent dosyası içerisinde "scripts" klasörü oluşturarak ps doyalarını içeri atıyoruz.

Agent.conf içerisine aşağıdaki gibi userparameter ekliyoruz;

UserParameter=windows.certs[*],powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Program Files\zabbix-agent\scripts\windows_certs.ps1" -ActionType "$1" -Key "$2" -Value "$3"

Template'i hosta assing ettiğimizde otomatik discovery ederek item-triggerları oluşturuyor.

İtemlar;

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" days to expire

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" expire date

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" issued by

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" issued date


Triggerlar;
Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" is expired	

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" is expiring today	

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" is expiring to {$WINDOWS_CERT_DAYS_TO_EXPIRE_AVERAGE} days ({ITEM.LASTVALUE1} left)	

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" is expiring to {$WINDOWS_CERT_DAYS_TO_EXPIRE_INFO} days ({ITEM.LASTVALUE1} left)

Certificate "{#LM_CERT_CN} ({#LM_CERT_FRIENDLYNAME})" is expiring to {$WINDOWS_CERT_DAYS_TO_EXPIRE_WARN} days ({ITEM.LASTVALUE1} left)	


$WINDOWS_CERT_DAYS_TO_EXPIRE_AVERAGE template içerisinde makrolardan belirlenip özelleştirilebilir.

![image](https://user-images.githubusercontent.com/85514498/193828763-a38fa44a-c345-4c68-b248-a4d2cbde53d9.png)


Zabbix v5.0.10 ve Agent v5 test edildi.
