# Debloat Windows 10

This project collects PowerShell scripts which help to *debloat* Windows 10,
tweak common settings and install basic software components.

I test these scripts on a Windows 10 Professional 64-Bit (English) virtual
machine. Please let me know if you encounter any issues. Home Edition and
different languages are not supported. These scripts are intended for
tech-savvy administrators, who know what they are doing and just want to
automate this phase of their setup. If this profile does not fit you, I
recommend using a different (more interactive) tool -- and there are a lot of
them out there.

Also, note that gaming-related apps and services will be removed/disabled. If
you intend to use your system for gaming, adjust the scripts accordingly.

**There is no undo**, I recommend only using these scripts on a fresh
installation (including Windows Updates). Test everything after running them
before doing anything else. Also, there is no guarantee that everything will
work after future updates since I cannot predict what Microsoft will do next.


## Execution

Enable execution of PowerShell scripts:

    PS> Set-ExecutionPolicy Unrestricted -Scope CurrentUser

Unblock PowerShell scripts and modules within this directory:

    PS> ls -Recurse *.ps*1 | Unblock-File

## Usage

Scripts can be run individually, pick what you need.

1. Install all available updates for your system.
2. Edit the scripts to fit your need.
3. Run the scripts you want to apply from a PowerShell with administrator privileges (Explorer
   `Files > Open Windows PowerShell > Open Windows PowerShell as
   administrator`)
4. `PS > Restart-Computer`
5. Run `disable-windows-defender.ps1` one more time if you ran it in step 3
6. `PS > Restart-Computer`

## Start menu

If the start menu stops working for whatever reason, you can install these mods for them

[Open Shell]: <https://open-shell.github.io/Open-Shell-Menu/>
[Start is Back]: <http://startisback.com/>

### Start menu Search

After running the scripts, the start menu search-box may no longer work on newly
created accounts. It seems like there is an issue with account initialization
that is triggered when disabling the GeoLocation service. Following workaround
has been discovered by BK from Atlanta:

1. Delete registry key `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\lfsvc\TriggerInfo\3`
2. Re-enable GeoLocation service (set startup type to `Automatic`)
3. Reboot
4. Login with the account having the stated issue
5. Start Cortana and set your preferences accordingly (web search and whatnot)

You may now disable the GeoLocation service again, the search box should remain
functional.

### Sysprep will hang

If you are deploying images with MDT and running these scripts, the sysprep
step will hang unless `dmwappushservice` is active.

### Xbox Wireless Adapter

Apparently running the stock `remove-default-apps` script will cause Xbox
Wireless Adapters to stop functioning. I suspect one should not remove the Xbox
App when wanting to use one. But I haven't confirmed this yet, and there is a
workaround to re-enable it afterwards. See
[#78](https://github.com/W4RH4WK/Debloat-Windows-10/issues/78).

### Issues with Skype

Some of the domains blocked by adding them to the hosts-file are required for
Skype. I highly discourage using Skype, however some people may not have
the option to use an alternative. See the
[#79](https://github.com/W4RH4WK/Debloat-Windows-10/issues/79).

### Fingerprint Reader / Facial Detection not Working

Ensure *Windows Biometric Service* is running. See
[#189](https://github.com/W4RH4WK/Debloat-Windows-10/issues/189).

## Liability

**All scripts are provided as-is and you use them at your own risk.**

