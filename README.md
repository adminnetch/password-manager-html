# 🚀 Installazione Facile - Password Manager

## 📋 Requisiti
- Server web con PHP (XAMPP, WAMP, o server Linux)
- MariaDB/MySQL database
- Browser moderno

## 🔧 Setup in 5 minuti

### 1. Scarica e posiziona i file
```
password-manager/
├── index.html          (il tuo file HTML)
├── api.php            (il file PHP che ho creato)
└── config.php         (opzionale, per configurazioni)
```

### 2. Configura il database
Apri `api.php` e modifica queste righe:
```php
$host = 'localhost';           // IP del tuo MariaDB
$dbname = 'password_manager';  // Nome database
$username = 'your_username';   // Il tuo username MariaDB  
$password = 'your_password';   // La tua password MariaDB
```

### 3. Crea il database
Nel tuo MariaDB, esegui:
```sql
CREATE DATABASE password_manager;
```
(La tabella si creerà automaticamente al primo avvio)

### 4. **IMPORTANTE - Cambia la chiave di crittografia!**
In `api.php`, trova questa riga e cambiala:
```php
$encryption_key = 'your-secret-key-change-this-123456789';
```
Metti una chiave lunga e complessa, tipo:
```php
$encryption_key = 'MiaChiaveSegreta2024!@#$%SuperLunga';
```

### 5. Avvia il server web
- **XAMPP/WAMP**: Metti i file nella cartella `htdocs`
- **Server Linux**: Metti nella cartella web (es. `/var/www/html`)

### 6. Apri nel browser
Vai su: `http://localhost/password-manager/`

## 🛡️ Sicurezza

### Password Crittografate
Le password sono crittografate con AES-256-CBC nel database.

### Suggerimenti di sicurezza:
- ✅ Usa HTTPS in produzione  
- ✅ Cambia la chiave di crittografia
- ✅ Backup regolari del database
- ✅ Limita l'accesso alla rete locale
- ✅ Usa utenti database con privilegi limitati

## 🔧 Struttura Database
```sql
CREATE TABLE servers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    ip VARCHAR(45) NOT NULL,
    type ENUM('web', 'database', 'mail', 'file', 'backup', 'other'),
    port INT,
    username VARCHAR(255) NOT NULL,
    password_encrypted TEXT NOT NULL,  -- AES encrypted
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 🚨 Risoluzione Problemi

### Errore di connessione database:
1. Verifica che MariaDB sia avviato
2. Controlla IP, username e password in `api.php`  
3. Verifica che l'utente abbia i permessi sul database

### L'app usa dati locali invece del database:
- Controlla la console del browser (F12)
- L'app funziona lo stesso, ma salva nel localStorage

### CORS errors:
- Assicurati di accedere via `http://localhost` non `file://`

## 📱 Funziona anche offline!
Se il database non è raggiungibile, l'app continua a funzionare salvando i dati localmente nel browser.
