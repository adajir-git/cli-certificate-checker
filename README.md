# CLI Certificate Checker

Simple terminal tool to quickly inspect an HTTPS/TLS certificate for a given domain.  
Shows certificate validity, issuer, common name, SANs and basic DNS info (A/AAAA records with PTR).

## Features

- Checks HTTPS certificate on port 443 using SNI.
- Shows status (VALID / WARNING / EXPIRED) based on remaining days.
- Prints validity period, common name (CN) and issuer.
- Resolves IPv4/IPv6 records and shows PTR for IPv4.
- Parses Subject Alternative Names and resolves their A records.

## Installation

```bash
git clone git@github.com:adajir-git/cli-certificate-checker.git
cd cli-certificate-checker
chmod +x checkcert
# optional: symlink into ~/bin so it's on PATH
ln -s "$PWD/checkcert" ~/bin/checkcert
```

Or clone via HTTPS if you do not use SSH keys:

```bash
git clone https://github.com/adajir-git/cli-certificate-checker.git
``` [web:90][web:93]

Requirements:

- `bash`
- `openssl`
- `dig` (from `bind-utils` / `dnsutils`)
- `curl`

## Usage

Basic usage:

```bash
checkcert example.com
```

Example output:

```text
Domain: example.com

Certificate:
  Status:        VALID (expires in 42 days)
  Valid From:    ...
  Valid To:      ...
  Common Name:   example.com
  Issuer:        ...
  Server:        nginx

IPv4:
  93.184.216.34     (PTR: ...)

IPv6:
  (no AAAA records)

Subject Alternative Names:
    - example.com                 93.184.216.34
    - www.example.com             93.184.216.34
    - *.example.net               wildcard
```

If the domain does not resolve (no A/AAAA records) or there is no HTTPS service on port 443, the script prints a clear error message and exits with a non-zero status. [web:119]

## License

MIT License – see [LICENSE](./LICENSE) for details.
