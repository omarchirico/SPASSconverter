# SPASS → CSV Converter

🇮🇹 [Italiano](#-italiano) · 🇬🇧 [English](#-english)

\---

## 🇮🇹 Italiano

Convertitore da **`.spass`** (esportazione di Samsung Pass) a **`.csv`**, per importare le tue password in Google Password Manager (o in altri gestori di password).

Funziona **interamente nel browser**: il file e la password non vengono mai inviati a nessun server.



### Lingue

L’interfaccia è in **italiano** (lingua predefinita) e disponibile in inglese, cinese, tedesco, spagnolo e francese: scegli la lingua dal menu in alto a destra. La scelta viene ricordata dal browser.



### Come si usa

1. Su Samsung Pass esporta i dati: otterrai un file `.spass` protetto da una password scelta da te.
2. Apri `spass-to-csv.html` nel browser (doppio clic o dalla pagina pubblicata).
3. Seleziona il file `.spass` e inserisci la password usata per l'esportazione.
4. Clicca **Converti e scarica CSV** e salva `password.csv`.
5. Importa il CSV in Google Password Manager: [passwords.google.com](https://passwords.google.com) → Impostazioni → Importa.
6. **Elimina il CSV** appena finito: contiene le password in chiaro.



### Formato del CSV

Il file generato usa le colonne richieste da Google:

```
name,url,username,password,note
```

### Voci con URL non valido

Google accetta solo indirizzi che iniziano con `https://`. Il convertitore sistema automaticamente le voci problematiche:

|Caso nel file `.spass`|Risultato nel CSV|
|-|-|
|App Android (`android://codice@com.facebook.katana/`)|`https://facebook.com/`, con il pacchetto salvato in *name* e *note*|
|Solo un nome (es. `Amazon`)|`https://www.amazon.com/`, con il valore originale in *note*|
|Dominio senza protocollo (es. `example.com`)|`https://example.com`|
|URL mancante|`https://www.example.com/`, con la nota `\[URL mancante]`|

Il dominio ricavato è una stima: se serve, dopo l'importazione puoi correggere l'indirizzo delle singole voci.



### Come funziona

Il formato `.spass` non è documentato ufficialmente da Samsung. Il convertitore segue ciò che è noto dalla community:

* il file è codificato in Base64: i primi 20 byte sono il *salt*, i 16 successivi l'*IV*, il resto è il testo cifrato;
* la chiave AES-256 deriva dalla password con PBKDF2-HMAC-SHA256 (70.000 iterazioni);
* la cifratura è AES-CBC, gestita dalla Web Crypto API del browser;
* il testo decifrato contiene una tabella con i campi (`origin\_url`, `username\_value`, `password\_value`, …) codificati in Base64.

Se Samsung cambia il formato, la conversione potrebbe non funzionare: apri una *issue* indicando solo il messaggio di errore, **senza allegare password o file reali**.



### Sicurezza

* Nessuna richiesta di rete: tutto il lavoro avviene in locale.
* Il CSV non è cifrato: conservalo il meno possibile ed eliminalo dopo l'importazione (svuota anche il cestino).
* Usa il convertitore solo con i tuoi dati.



### Avvertenze

Progetto indipendente, non affiliato né approvato da Samsung o Google. *Samsung Pass* e *Google* sono marchi dei rispettivi proprietari. Il software è fornito «così com'è», senza garanzie.





\--------------------------------------------------------------------------------------------------------------------------------



## 🇬🇧 English

A converter from **`.spass`** (Samsung Pass export) to **`.csv`**, so you can import your passwords into Google Password Manager (or other password managers).

It runs **entirely in your browser**: your file and password are never sent to any server.



### Languages

The interface is in **Italian** (default) and also available in English, Chinese, German, Spanish and French: pick the language from the menu at the top right. Your choice is remembered by the browser.



### How to use

1. In Samsung Pass, export your data: you will get a `.spass` file protected by a password you choose.
2. Open `spass-to-csv.html` in your browser (double-click it or use the published page).
3. Select the `.spass` file and enter the password you used for the export.
4. Click **Convert and download CSV** and save `password.csv`.
5. Import the CSV into Google Password Manager: [passwords.google.com](https://passwords.google.com) → Settings → Import.
6. **Delete the CSV** when you are done: it contains your passwords in plain text.



### CSV format

The generated file uses the columns Google expects:

```
name,url,username,password,note
```

### Entries with an invalid URL

Google only accepts addresses starting with `https://`. The converter automatically fixes problematic entries:

|Case in the `.spass` file|Result in the CSV|
|-|-|
|Android app (`android://hash@com.facebook.katana/`)|`https://facebook.com/`, with the package name kept in *name* and *note*|
|Name only (e.g. `Amazon`)|`https://www.amazon.com/`, with the original value in *note*|
|Domain without protocol (e.g. `example.com`)|`https://example.com`|
|Missing URL|`https://www.example.com/`, with the note `\[URL mancante]`|

The derived domain is a best guess: after importing, you can edit the URL of individual entries if needed.



### How it works

The `.spass` format is not officially documented by Samsung. The converter follows what is known from the community:

* the file is Base64-encoded: the first 20 bytes are the *salt*, the next 16 the *IV*, the rest is the ciphertext;
* the AES-256 key is derived from the password with PBKDF2-HMAC-SHA256 (70,000 iterations);
* encryption is AES-CBC, handled by the browser's Web Crypto API;
* the decrypted text contains a table whose fields (`origin\_url`, `username\_value`, `password\_value`, …) are Base64-encoded.

If Samsung changes the format, conversion may stop working: please open an *issue* with the error message only, **without attaching real passwords or files**.



### Security

* No network requests: all processing happens locally.
* The CSV is not encrypted: keep it for as short a time as possible and delete it after importing (empty the recycle bin too).
* Only use the converter with your own data.



### Disclaimer

Independent project, not affiliated with or endorsed by Samsung or Google. *Samsung Pass* and *Google* are trademarks of their respective owners. The software is provided "as is", without warranty of any kind.

