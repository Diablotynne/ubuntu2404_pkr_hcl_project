# 🐧 Ubuntu 24.04 Vagrant Boxes

Ce dépôt contient les fichiers [Packer](https://www.packer.io/) nécessaires à la construction de boxes **Vagrant** pour **Ubuntu 24.04**, compatibles avec les architectures **AMD64** et **ARM64**.

---

## 🛠️ Construction des boxes

### 🔧 Dépendances Packer

Initialiser les fichiers Packer :
```bash
packer init ubuntu-amd64.pkr.hcl
```

### ⚙️ Construire la box AMD64
```bash
packer build -var-file="amd64.pkrvars.hcl" ubuntu-amd64.pkr.hcl
```

### 🐞 Mode débogage
```bash
PACKER_LOG=debug PACKER_LOG_PATH=ubuntu.log \
packer build -var-file="amd64.pkrvars.hcl" ubuntu-amd64.pkr.hcl
```

Les artefacts sont générés dans le dossier `output-vagrant/`.

---

## 🧪 Tester la box Vagrant

### 📦 Installation locale
```bash
vagrant box add ubuntu_24_04 output-vagrant/ubuntu-24-04-amd64.box
```

### 🚀 Initialiser un projet de test
```bash
mkdir vagrant_project && cd vagrant_project
vagrant init ubuntu_24_04
vagrant up --provider virtualbox
```

---

## 🚧 ARM64 – Configuration Spécifique (MacOS Silicon)

⚠️ VirtualBox ne permet pas l’export OVF sur MacOS avec ARM64.  
Utiliser la méthode manuelle pour créer la box :

```bash
cd output-vagrant
tar -czf ubuntu-24-04-arm64.box ./metadata.json ./Vagrantfile ./box.ovf ./ubuntu-24-04-arm64-disk001.vmdk
```

### 📥 Ajouter la box ARM64
```bash
vagrant box add ubuntu_24_04 output-vagrant/ubuntu-24-04-arm64.box
```

### 🧼 Nettoyage de l’environnement
```bash
cd ..
vagrant box remove ubuntu_24_04
rm -rf vagrant_project/
```

### 🧹 Supprimer les disques VirtualBox
```bash
VBoxManage list hdds
VBoxManage closemedium disk ${disk_uuid} --delete
```

---

## 📚 Ressources

- [Documentation Packer](https://developer.hashicorp.com/packer/docs)
- [Documentation Vagrant](https://developer.hashicorp.com/vagrant/docs)

---

## 📝 Licence

Ce projet est sous licence MIT.

---

Happy building! 🎉

