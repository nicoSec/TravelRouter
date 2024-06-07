<h1>Travel VPN Router w/ Wifi</h1>

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
        <li><strong>Download OpenWrt:</strong> Go to the <a href="https://openwrt.org/">OpenWrt website</a> and download the latest stable release for the Raspberry Pi 4B. Ensure you select the correct version to avoid compatibility issues.</li>
        <li><strong>Flash OpenWrt to the MicroSD Card:</strong>
            <ul>
                <li><em>Format the MicroSD Card:</em> Use a tool like <a href="https://www.sdcard.org/downloads/formatter/">SD Card Formatter</a> to format the microSD card.</li>
                <li><em>Flash the Image:</em> Use a tool like <a href="https://www.raspberrypi.com/software/">Raspberry Pi Imager</a> to flash the downloaded OpenWrt image onto the microSD card. Insert the microSD card into your computer, and open Raspberry Pi Imager. Select Raspberry Pi 4 as the Raspberry Pi Device, the OpenWrt image for the Operating System, and your SD Card for Storage and click "Next". You might be asked if you want to apply custom settings, click "No" and your SD card will be flashed with OpenWrt.</li>
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
                <li><em>Connect to the Raspberry Pi:</em> On your computer, log into the Pi via SSH using the default IP address for OpenWrt, <code>root@192.168.1.1</code>.</li>
            </ul>
        </li>
    </ol>
