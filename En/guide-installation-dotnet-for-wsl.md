# 🧩 Installing .NET on WSL (Ubuntu)  

This guide shows how to install the .NET SDK on WSL with Ubuntu.  

---  

## ✅ Step 1: Update packages  

```bash  
sudo apt update && sudo apt upgrade -y  
```  

---  

## ✅ Step 2: Install prerequisites  

```bash  
sudo apt install -y wget apt-transport-https software-properties-common  
```  

---  

## ✅ Step 3: Add the Microsoft repository  

```bash  
wget https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb  
sudo dpkg -i packages-microsoft-prod.deb  
rm packages-microsoft-prod.deb  
```  

---  

## ✅ Step 4: Update packages again and install the .NET SDK  

```bash  
sudo apt update  
sudo apt install -y dotnet-sdk-8.0  
```  

> 🔄 You can replace `dotnet-sdk-8.0` with `dotnet-sdk-7.0` or `dotnet-sdk-6.0` as needed.  

---  

## ✅ Step 5: Verify the installation  

```bash  
dotnet --version  
```  

If it returns the .NET version, the installation was successful! ✅  

---  

## (Optional) Install ASP.NET Core Runtime  

If you need to run web applications:  

```bash  
sudo apt install -y aspnetcore-runtime-8.0  
```  

---  

## 📝 Note  

These commands work on Ubuntu in WSL 2. Make sure your distro is up to date.