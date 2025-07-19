# osint-password-email-
├── .gitignore
├── README.md
├── LICENSE
├── install_tools.sh
├── run_holehe.sh
├── run_john.sh
├── run_hydra.sh
└── run_hashcat.sh

venv/
*.json
*.html

# osint-password-email

Repositório para estudos de auditoria de senhas e investigação de e‑mails em ambientes controlados.

## Aviso Legal
Uso restrito a sistemas sob sua responsabilidade e para fins educacionais.

## Instalação
```bash
git clone https://github.com/SEU_USUARIO/osint-password-email.git
cd osint-password-email
chmod +x *.sh
./install_tools.sh

Uso

Holehe: ./run_holehe.sh seu.email@exemplo.com

John the Ripper: ./run_john.sh hashes.txt

Hydra: ./run_hydra.sh -l usuario -P wordlist.txt ssh://host

Hashcat: ./run_hashcat.sh hashes.txt wordlist.txt


#!/usr/bin/env bash
set -e

# Atualiza sistema e instala dependências
sudo apt update && sudo apt install -y \
  python3-venv python3-pip git hashcat john hydra pipx curl

# Instala Holehe via pipx
pipx install holehe
# Ajusta PATH para pipx
pipx ensurepath

#!/usr/bin/env bash
# Usa John the Ripper para cracking de hashes
# Exemplo de uso: ./run_john.sh hashes.txt
HASHFILE="$1"
if [[ -z "$HASHFILE" ]]; then
  echo "Uso: ./run_john.sh hashes.txt"
  exit 1
fi
john --wordlist=rockyou.txt "$HASHFILE"

#!/usr/bin/env bash
# Executa Hydra para brute-force em serviços
# Exemplo de uso: ./run_hydra.sh -l usuario -P wordlist.txt ssh://host
if [[ $# -lt 1 ]]; then
  echo "Uso: ./run_hydra.sh [options] target"
  exit 1
fi

ohydra "$@"

#!/usr/bin/env bash
# Executa Hashcat para cracking de senhas via GPU/CPU
# Exemplo de uso: ./run_hashcat.sh hashes.txt wordlist.txt
HASHFILE="$1"
WORDLIST="$2"
if [[ -z "$HASHFILE" || -z "$WORDLIST" ]]; then
  echo "Uso: ./run_hashcat.sh hashes.txt wordlist.txt"
  exit 1
fi
hashcat -m 0 "$HASHFILE" "$WORDLIST"
