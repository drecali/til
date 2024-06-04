# App recommendation: Coconut Battery

Coconut Battery is a free app that shows you the current battery health of your MacBook. It shows:

- the current battery capacity,
- the original battery capacity,
- the current charge,
- the battery cycles,
- battery temperature,
- battery power usage,
- power adapter info,
- and more.

vIt's a great way to keep track of your battery health and to see if you need to replace your battery. It's a must-have app for any MacBook user.

![image](https://github.com/drecali/til/assets/24983797/d9cfd450-2e0e-4453-bff6-f1bb39257d78)

You can download it from [coconut-flavour.com](https://coconut-flavour.com/coconutbattery/).

## Note

Some people [don't trust](https://www.reddit.com/r/MacOS/comments/17rg0sf/is_coconut_battery_unreliable/?rdt=52398) Coconut Battery but you can easily verify its accuracy with one simple terminal command. Check out [Get MacBook battery info with terminal command](./get-macbook-battery-info-with-terminal-command.md) for more information. You'll see the terminal command output and Coconut Battery have identical values.

If you're too lazy to check the other page, here's the command:

```bash
ioreg -l |grep -e '"DesignCapacity" =' -e '"AppleRawMaxCapacity" =' -e '"AppleRawCurrentCapacity" ='
```
