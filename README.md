<h1>Travel VPN Router w/ Wifi AP</h1>

<h2>Description</h2>
Creating a portable router can be a game-changer for anyone seeking secure, private internet access on the go. In this project, I'll walk you through how I transformed a Raspberry Pi 4 into a portable router using OpenWrt and the IPVanish. The best part? It’s flexible and can be used with various VPN services, not just IPVanish. Whether you're a digital nomad, frequent traveler, or just someone who values online privacy, this guide will help you build a reliable and portable solution to keep your internet connections secure and private, no matter where you are. Let's dive into the step-by-step process of setting up this powerful device and unlock the full potential of your Raspberry Pi 4.
</br>

<h2>Hardware Requirements</h2>
	<ul>
		<li>Raspberry Pi 4b: The central piece of hardware for your portable router.</li>
		<li>MicroSD Card (16GB or higher: For storing the OpenWrt operating system and configuration files.</li>
		<li>Power Supply: A reliable power source for your Raspberry Pi 4.</li>
		<li>Ethernet Cable: For connecting the Raspberry Pi to a wired network.</li>
		<li>Wireless WiFi USB Adapter: To enable WiFi on your Raspberry Pi router.</li>
		<li>Portable Power Bank (optional): To make your router truly portable.</li>
		<li>Case for Raspberry Pi (optional): To protect your hardware during travel.</li>
	</ul>

<h2>Software Requirements</h2>
  <ul>
    <li>OpenWrt Firmware: The open-source firmware that will turn your Raspberry Pi into a powerful router.</li>
    <li>IPVanish VPN Service: To ensure secure and private internet access. Other VPN services will also work.</li>
    <li>SD Card Formatter: Software to format your microSD card before installing OpenWrt.</li>
    <li>Etcher or Raspberry Pi Imager: For flashing the OpenWrt firmware onto your microSD card.</li>
    <li>SSH Client (e.g., PuTTY): To remotely access and configure your Raspberry Pi.</li>
  </ul>

With these requirements in hand, you’ll be well-equipped to build your own portable router and enjoy secure, private browsing wherever you go.



<h1>Step 1: Preparing the Raspberry Pi</h1>
      <ol>
        <li><strong>Gather Your Materials:</strong> Ensure you have all necessary components: Raspberry Pi 4B, microSD card (at least 8GB), power supply, Ethernet cable, wireless USB adapter, and a computer for setup.</li>
        <li><strong>Download OpenWrt:</strong> Go to the <a href="https://openwrt.org/">OpenWrt website</a> and download the latest stable release for the Raspberry Pi 4B. Ensure you select the current stable release to avoid compatibility issues.</li>
        <li><strong>Flash OpenWrt to the MicroSD Card:</strong>
            <ul>
                <li><em>Format the MicroSD Card:</em> Use a tool like <a href="https://www.sdcard.org/downloads/formatter/">SD Card Formatter</a> to format the microSD card.</li>
                <li><em>Flash the Image:</em> Use a tool like <a href="https://www.raspberrypi.com/software/">Raspberry Pi Imager</a> to flash the downloaded OpenWrt image onto the microSD card. Insert the microSD card into your computer, and open Raspberry Pi Imager. Select Raspberry Pi 4 as the Raspberry Pi Device, the OpenWrt image for the Operating System, and your SD Card for Storage and click "Next". You might be asked if you want to apply custom settings, click "No" and your SD card will be flashed with OpenWrt.</li>
		    <img src="https://i.imgur.com/AikaSN8.png" height="50%" width="50%" alt="Raspbery Pi Imager">
            </ul>
        </li>
        <li><strong>Insert the MicroSD Card:</strong> Once the flashing process is complete, remove the microSD card from your computer and insert it into the Raspberry Pi 4B.</li>
        <li><strong>Connect the Raspberry Pi:</strong>
            <ul>
                <li><em>Ethernet:</em> Connect one end of the Ethernet cable to your Raspberry Pi and the other end to your computer.</li>
                <li><em>Power:</em> Plug in the power supply to the Raspberry Pi and then to a power outlet.</li>
            </ul>
        </li>
        <li><strong>Initial Setup:</strong>
            <ul>
                <li><em>Connect to the Raspberry Pi:</em> On your computer, log into the Pi via SSH using the default IP address for OpenWrt, <code>root@192.168.1.1</code>. Assuming your home router is not using 192.168.1.1 as its IP address already, you should have no issue loggin into your pi this way. In case it is, there are several work arounds. The easiest in my opinion is to simply disconnect from home router and then logging into your Raspberry Pi.</li>
		<img src="https://i.imgur.com/uZVwlMP.png" height="50%" width="50%" alt="OpenWrt">
            </ul>
        </li>
    </ol>

<h1>Step 2: Configuring the Raspberry Pi</h1>
	<ol>
		<li><strong>Change the Root Password:</strong> The first thing you should do is change your root password by entering the <code>passwd</code> command. </li>
		<li><strong>Back Up Config Files:</strong> Before making changes to our config files, lets back them up in case we need to revert back to factory settings.</li>
			<ul>
				<code>cd /etc/config</code><br>
				<code>cp firewall firewall.bk</code><br>
				<code>cp wireless wireless.bk</code><br>
				<code>cp network network.bk</code>
			</ul>
		<li><strong>Configure the Nework File:</strong></li>
			<ul>
				<li>Having made the back up files of our config files, we can now begin to customize them to get our router working by entering the command <code>vi network</code>. Update the 'lan' interface and add the 'wwan', and 'vpnclient' interfaces to the file as shown below. Remember when choosing your own IP address for the 'lan' interface, make sure it is within a private IP address range.</li>
				<li>Since we are using Vim to edit the file, hit the letter 'i' on your keyboard to begin and once your done, 'esc' key and type ':wq' to save your work and close Vim.</li>
				<img src="https://i.imgur.com/qXvEXyf.png" height="50%" width="50%" alt="Network File">
			</ul>
		<li><strong>Configure the Firewall File:</strong> </li>
			<ul>
				<li>Similar to what we did in the network file, we will also edit the firewall file, but we will only be changing one value. We will change option input 'REJECT' to 'ACCEPT' under config zone 'wan'. <code>vi firewall</code> will open our file, 'i' key to make our update, and 'esc' key then ':wq' to save and exit.</li>
				<img src="https://i.imgur.com/RqWwOkW.png" height="50%" width="50%" alt="Firewall File">
				<li>You have now successfully updated the necessary config files, now reboot the pi with the <code>reboot</code> command and continue onto the next step.</li>
			</ul>
	</ol>

<h1>Step 3: Wireless Configuration</h1>
	<ol>
		<li><strong>Configuring the Pi's Internal Wifi:</strong> Log back into your Pi using the IP address you picked in the network config file <code>ssh root@[IP ADDRESS]</code>. </li>
			<ul>
				<li><code>cd /etc/config</code></li>
				<li><code>vi wireless</code></li>
				<li>Update config wifi-device 'radio0' to use the settings below:</li>
				<img src="https://i.imgur.com/YbI5RD6.png" height="50%" width="50%" alt="radio0">
				<li><code>uci commit wireless</code></li>
				<li><code>wifi</code></li>
				<li>You can verify you completed this step successfully if you see "OperWrt" as an availiable Wifi network.</li>
			</ul>
		<li><strong>Connecting to the Internet:</strong> Use your browser to log into the Raspberry Pi to scan for your home network. Simply enter the Pi's IP address you set up in the network config file in the searchbar and log in using the same password used to SSH into the Pi. </li>
			<ul>
				<li>Click on Network > Wireless then using the 'radio0' click 'Scan'</li>
				<li>Log into your your Wifi network and make sure to mark 'Replace wireless configuration', then click Save.</li>
				<img src="https://i.imgur.com/abdxFvg.png" height="50%" width="50%" alt="Wifi">
				<li>Click "Save & Apply".</li>
				<li>Your Raspberry Pi is now a functioning router, however it is not secured just yet. I would not recommend stopping here as the whole purpose of this project is to add security to your Internet access while traveling.</li>
			</ul>
		<li><strong>Download Tools and Drivers:</strong> The external USB wireless adapter will be used as out Access Point for our router. We can't simply plug-and-play, we will need to download some additional tools and drivers to enhance our Pi's abilities.</li>
			<ul>
				<li>Back in the command line, enter these commands:</li>
				<li><code>opkg update</code></li>
				<li><code>opkg install kmod-rt2800-lib kmod-rt2800-usb kmod-rt2x00-lib kmod-rt2x00-usb kmod-usb-core kmod-usb-uhci kmod-usb-ohci kmod-usb2 usbutils openvpn-openssl luci-app-openvpn</code></li>
				<li>A quick <code>reboot</code> after this wouldn't hurt either.</li>
			</ul>
		<li><strong>Setting Up the Wifi AP:</strong> It is important to use the tools available to us and here we will be adding Wifi to our router using the external USB Wireless adapter.</li>
			<ul>
				<li>Run <code>lsusb</code> before and after plugging in your USB Wireless adapter. It's not required but you will see that the Pi has identified the adapter.</li>
				<li>Once the USB Wirelss adapter is plugged in run <code>ifconfig wlan1 up</code></li>
				<li>Update the wireless config file to apply your own wifi SSID and password.</li>
				<li><code>vi /etc/config/wireless</code></li>
				<img src="https://i.imgur.com/opUXLvB.png" height="50%" width="50%" alt="Wifi Config">
				<li><code>uci commit wireless</code></li>
				<li><code>wifi</code></li>
			</ul>	
	</ol>
 <h1>Step 4: VPN Configuration</h1>
 	<ol>
		<li><strong>VPN Config Files:</strong> Download your VPN config file from your VPN service provider. Additionally, download the certificate file, as it is required when using IPVanish. These will have .ovpn and .crt file extensions. If you are using IPVanish, you can find both in the <a href="https://configs.ipvanish.com/configs/">IPVanish Configs</a> website</li>
			<ul>
				<li>From your Downloads folder we will send both of these files to your Raspberry Pi using scp.</li>
				<li><code>scp [name of VPN config file.ovpn] root@[PI's IP Adress]:/etc/openvpn/client.conf</code> if you entered this command correctly, you will be asked to enter your Pi's password.</li>
				<li><code>scp [name of certificate.crt] root@[PI's IP Adress]:/etc/openvpn/[name of certificate.crt]</code> if you entered this command correctly, you will be asked to enter your Pi's password.</li>
			</ul>
		<li><strong>Install VPN Packages:</strong> Run these commands.</li>
			<ul>
				<li><code>opkg update</code></li>
				<li><code>opkg install luci-app-openvpn</code></li>
				<li><code>/etc/init.d/rpcd restart</code></li>
			</ul>
		<li><strong>Configure VPN Parameters</strong> Run these commands.</li>
			<ul>
				<li><code>OVPN_DIR="/etc/openvpn"</code></li>
				<li><code>OVPN_ID="client"</code></li>
				<li><code>OVPN_USER="VPN USERNAME/EMAIL"</code> (enter your own VPN Login ID)</li>
				<li><code>OVPN_PASS="PASSWORD"</code> (enter your VPN Login password)</li>
			</ul>
		<li><strong>VPN Credentials Script:</strong> Copy this script and run it in your Pi's command line.</li>
			<ul>	
				<li>umask go=<br>
				cat << EOF >${OVPN_DIR}/${OVPN_ID}.auth<br>
				${OVPN_USER}<br>
				${OVPN_PASS}<br>
				EOF<br></li>
			</ul>
		<li><strong>VPN Instance Management Script:</strong> Copy this script and run it in your Pi's command line.</li>
			<ul>	
				<li>sed -i -e "<br>
				/^auth-user-pass/s/^/#/<br>
				\$a auth-user-pass ${OVPN_ID}.auth<br>
				/^redirect-gateway/s/^/#/<br>
				\$a redirect-gateway def1 ipv6<br>
				" ${OVPN_DIR}/${OVPN_ID}.conf<br></li>
				<li><code>/etc/init.d/openvpn restart</code></li>
			</ul>
		<li><strong>VPN Service Script:</strong> Copy this script and run it in your Pi's command line.</li>
			<ul>	
				<li>ls /etc/openvpn/*.conf \<br>
				| while read -r OVPN_CONF<br>
				do<br>
				OVPN_ID="$(basename ${OVPN_CONF%.*} | sed -e "s/\W/_/g")"<br>
				uci -q delete openvpn.${OVPN_ID}<br>
				uci set openvpn.${OVPN_ID}="openvpn"<br>
				uci set openvpn.${OVPN_ID}.enable="1"<br>
				uci set openvpn.${OVPN_ID}.config="${OVPN_CONF}"<br>
				done<br>
				uci commit openvpn<br></li>
				<li><code>/etc/init.d/openvpn restart</code></li>
			</ul>
		<li><strong>Firewall Configuration Script:</strong> Copy this script and run it in your Pi's command line.</li>
			<ul>	
				<li>ci rename firewall.@zone[0]="lan"<br>
				uci rename firewall.@zone[1]="wan"<br>
				uci del_list firewall.wan.device="tun+"<br>
				uci add_list firewall.wan.device="tun+"<br>
				uci commit firewall<br></li>
				<li><code>/etc/init.d/firewall restart</code></li>
			</ul>
		<li><strong>Hotplug Configuration Script:</strong> Copy this script and run it in your Pi's command line.</li>
			<ul>	
				<li>mkdir -p /etc/hotplug.d/online<br>
				cat << "EOF" > /etc/hotplug.d/online/00-openvpn<br>
				/etc/init.d/openvpn restart<br>
				EOF<br>
				cat << "EOF" >> /etc/sysupgrade.conf<br>
				/etc/hotplug.d/online/00-openvpn<br>
				EOF</li><br>
			</ul>
	</ol>
