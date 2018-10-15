# usb-yazma-koruma
#Bu shell script kod parçacığı usb portunun yazma korumalı hale getirilmesini sağlar
#!/bin/bash
#gsettings, lsblk, mount
 
while :
do
 
read -p "Otomatik bağlama kapatılsın mı?(e/h): " cevap if [ "$cevap" == "e" ]
then gsettings set org.gnome.desktop.media-handling automount false echo "Otomatik bağlama kapatıldı." read -p "Cihazı takınız(enter): " cevap if [ "$cevap" == "" ]
then
lsblk  --output name,vendor,model,hotplug,SERIAL,STATE break
fi
break
elif [ "$cevap" == "h" ]
then gsettings set org.gnome.desktop.media-handling automount true
echo "Otomatik bağlama aktif edildi." break
else echo "Yanlış girdi."
fi
done while :
do
read -p "Bağlanacak aygıt ya da bölüm: " aygit
read -p "Bağlanılacak dizinin tam yolu(Varsayılan /root/bagla): " dizin if [ "" == "$dizin" ] then dizin=/root/bagla
else mkdir -p $dizin
fi
mount -r /dev/$aygit $dizin break
done
