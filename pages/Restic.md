- Restic é um software rápido e seguro de backup.
  Documentação: https://restic.readthedocs.io/en/stable/
-
- ## Instalando
- **Debian**:
  ```
  apt-get install restic
  ```
- **RHEL & CentOS**
  ```
  dnf install epel-release
  dnf install restic
  ```
-
- > No caso do HPC Marvin, foi feito o download da última release estável no repositório do restic no GitHub.
-
- ## Capabilities para o binário
- Como no cenário do HPC, lidamos com filesystems via NFS ou Lustre, está configurado o squash root neles. Ou seja, ao rodar comandos como root ou com sudo nos nós do HPC, nos mountpoints o UID é mapeado para um usuário non-root.
- Para contornar isso, utilizamos as [[Linux Capabilities]] no binário do Restic para conceder algumas permissões.
	- Atualmente, estão aplicadas as seguintes caps no executável do Restic:
		- `cap_chown`
		- `cap_dac_override`
		- `cap_fowner`
-
-
- ## Preparando um novo repositório
- `restic init --repo <caminho do repo>`
-
- ## Relizando o backup
- `restic -r <caminho do repo> --verbose backup <caminho a ser feito backup>`
-
- ## Restaurando backups
- `restic -r /ibira/lnbio/backups/edb/restic-home2 restore latest --target / --include /home/jose.pereira/.boltz`