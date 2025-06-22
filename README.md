# phpIPAM 1.4.5 - Remote Code Execution (RCE) (Authenticated)

* **EDB-ID:** 50963 
* **Author:** [Guilherme Alves](https://github.com/behindsecurity)
* **Date:** 2022-06-14 
* **Platform:** PHP

## Description

This exploit leverages an authenticated SQL-injection vulnerability in phpIPAM version 1.4.5 to achieve remote code execution. A valid account in phpIPAM is required to trigger the flaw and write a PHP web shell or execute arbitrary commands on the target server.

## Requirements

- Python 3
- Python packages:
  - `requests`
  - `argparse` (standard library)
  - `termcolor`
- Network access to the phpIPAM instance
- Valid phpIPAM credentials (username/password)
- Writable path on the target server where the web shell or payload will be saved

## Installation

1. Clone or download this directory to your attack machine.  
2. Install the required Python modules:

```bash
pip3 install requests termcolor
````

## Usage

```bash
python3 exploit.py \
  -url http://<target>/phpipam \
  -usr <username> \
  -pwd <password> \
  -cmd "<command_to_execute>" \
  --path <writable/path/on/server>/shell.php
```

* `-url`
  Base URL of the phpIPAM installation (e.g. `http://192.168.1.100/phpipam`).
* `-usr` and `-pwd`
  Valid phpIPAM username and password.
* `-cmd`
  OS command to execute on the server.
* `--path`
  Absolute or relative writable path on the target where the injected PHP payload or shell will be created (e.g. `/var/www/html/phpipam/shells/shell.php`).

### Example

```bash
python3 exploit.py \
  -url http://192.168.1.100/phpipam \
  -usr admin \
  -pwd P@ssw0rd123 \
  -cmd "id" \
  --path /var/www/html/phpipam/shells/shell.php
```

## Disclaimer

This code is provided for educational and authorized-testing purposes only. Unauthorized use against systems you do not own or have explicit permission to test is illegal and unethical. The author and Exploit-DB are not responsible for any misuse of this exploit.

## References

* Exploit-DB: [https://www.exploit-db.com/exploits/50963](https://www.exploit-db.com/exploits/50963)
* Vendor homepage: [https://phpipam.net/](https://phpipam.net/)
* Software release (v1.4.5): [https://github.com/phpipam/phpipam/releases/tag/v1.4.5](https://github.com/phpipam/phpipam/releases/tag/v1.4.5)
