# wireless-tips

The regulatory domain country code "00" (global/unset), limits the enabled channels and sometimes disables 5 GHz channels. To enable 5 GHz WiFi scanning and connectivity regardless of country regulations, the best approach is to manually set a specific regulatory domain (country code) that permits 5 GHz operation. Manually setting the regulatory domain to "US" or another country with 5 GHz enabled is the most straightforward way to unlock seeing 5 GHz networks on Ubuntu, bypassing the default country "00" restrictions.

`iw` is a modern Linux command-line tool used to configure and query Wi-Fi devices (wireless interfaces). It works with the nl80211 kernel interface, replacing older tools like `iwconfig`.
You can verify your wireless driver supports 5 GHz bands by running:
  ```
  iw list
  ```
  and look for supported frequencies in the 5 GHz range (like 5180 MHz, 5200 MHz, etc.) that are not disabled.

- If your 5 GHz frequencies show as disabled, it might be a driver or hardware limitation. In that case, try updating your wireless drivers or kernel.

`iw reg get` command prints the current Wi-Fi regulatory domain (regdom) your system is using. The regulatory domain determines:
 
- Allowed Wi-Fi frequencies (2.4 GHz, 5 GHz, 6 GHz bands)

- Allowed transmit power levels

- Allowed DFS channels

If the regulatory domain is set to country code "00" (global/unset), it can limit the enabled channels and sometimes disables 5 GHz channels. To enable 5 GHz WiFi scanning and connectivity regardless of country regulations, the best approach is to manually set a specific regulatory domain (country code) that permits 5 GHz operation. On Ubuntu 24.04:

- Set the regulatory domain manually to a country that allows 5 GHz channels by running:
  ```
  sudo iw reg set US
  ```
  This sets the regulatory domain to the US, which enables 5 GHz bands.

- To make this persistent after reboot, create or edit a file `/etc/modprobe.d/cfg80211.conf` and add (use sudo to create and edit the file):
  ```
  options cfg80211 ieee80211_regdom=US
  ```
  Then reboot the system.

- Check again with `iw reg get` to confirm the country code shows as "US".
