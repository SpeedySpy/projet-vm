
# Projet VM
- En binome avec : Biraveen SIVAHARAN et Alex CORCEIRO

# Le but de notre Projet

- RÃ©aliser un projet complet intÃ©grant les enseignements dispensÃ©s durant la session decours en utilisant les outils Ã©tudiÃ©s pendant le cursus, ou en y intÃ©grant des outils au choixet innovant.

# Par ou commencer ?

- Dans un premier temps nous devons prendre connaissance des technologie ainsi que les comprendre.

# Les technologies : 
- Vagrant : Pour la crÃ©ation de notre machine virtuelle grace Ã  l'aide d'un script qui permettra de nous crÃ©er la machine virtuelle de facon autonome.
- Ansible : Pour installer les logiciels de facon automatique grace Ã  l'aide  d'un script.
- Docker : Permettra de deployer notre application web.
- MongoDB : Base de donnÃ©e qui permettra de stocker les donnÃ©es des utilisateurs.
- React : Framework qui regroupe l'HTML,CSS et javascript qui nous permettra de concevoir notre future application.
- VMware : Logiciel pour crÃ©er nos machines virtuelles
- Ubuntu : SystÃ¨me dâ€™exploitation GNU/Linux fondÃ© sur Debian.
- Visual studio code : Environnement de dÃ©veloppement.

# 1ere partie : Ansible / Vagrant

# 1ere Ã©tape : Ansible
- Installation des technologies et des paquets en passant par ces commandes :

```
python3 â€“m pip install--user ansible
```
- S'assurer d'avoir la bonne version de ANSIBLE
```
ansible --version
```
- Le mettre Ã  jour
```
python3 -m pip install --upgrade --user ansible
```
# 2eme Ã©tapes : Configuration d'ansible
```
sudo apt update 
sudo apt install software-properties-common 
sudo add-apt-repository --yes --update ppa:ansible/ansible 
sudo apt install ansible
```
# 3eme Ã©tapes : Mise en place de vagrant
- Dans cette Ã©tape, nous allons mettre en place un vagrantfile qui va nous servir pour crÃ©er notre machine virtuelle distante. Pour cela voici le script :
```
 Vagrant.configure("2") do |config|
  # Configuration de la box
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.box_version = "202004.27.0"
  # Configuration de la machine virtuelle
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "bento/ubuntu-20.04"
    ubuntu.vm.provider "vmware_workstation" do |v| 
      v.memory = 2048
      v.cpus = 2
      v.gui = true
    end
  end
end
```
- Pour exÃ©cuter voici la commande :
```
vagrant up
```

- Le rÃ©sultat :
```
 La vm s'est crÃ©e d'aprÃ¨s les caractÃ©ristiques qu'on lui a fournis.
```

# 4eme Ã©tapes : Mise en place de Ansible

- Dans cette partie, nous allons mettre en place un playbook qui va nous permettre d'installer les logiciels qu'on souhaite de maniÃ¨re automatique dans notre vm grace Ã  son adresse IP pour faire lien. Voici le script :
 ```
---
- name: Installer Visual Studio Code
  hosts: 192.168.59.128
  become: true
  tasks:
    - name: TÃ©lÃ©charger la clÃ© GPG de Microsoft
      apt_key:
        url: https://packages.microsoft.com/keys/microsoft.asc
        state: present

    - name: Ajouter le dÃ©pÃ´t Visual Studio Code
      apt_repository:
        repo: "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
        state: present

    - name: Installer Visual Studio Code
      apt:
        name: code
        state: present
 ```

- Pour exÃ©cuter notre playbook :
```
ansible-playbook playbook.yml
```

# 2eme partie : Docker






