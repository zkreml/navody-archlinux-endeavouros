# Rsync – Efektivní nástroj pro synchronizaci a zálohování

## Co je Rsync?

**Rsync** je nástroj pro Linux a Unix, který umožňuje efektivní kopírování a synchronizaci souborů a adresářů mezi dvěma umístěními. Díky své rychlosti a flexibilitě je skvělý pro pravidelné zálohování a přenos dat.

### Výhody Rsync

- **Rychlost a efektivita**: Přenáší pouze změněné nebo nové soubory.
- **Flexibilita**: Umožňuje lokální i vzdálenou synchronizaci přes SSH.
- **Bezpečnost**: Možnost šifrovaného přenosu přes SSH.
- **Automatizace**: Lze snadno použít v shell skriptech nebo cron úlohách.

---

## Základní Syntaxe

```bash
rsync [volby] zdroj cíl
```

## Časté volby

- -a: Archivní režim (zachovává atributy jako vlastnictví, oprávnění atd.).
- -v: Verbose (zobrazuje podrobné informace o procesu).
-  -h: Human-readable (přehledné zobrazování velikostí)
-  -z: Komprimuje data během přenosu (pro zrychlení).
-  -e ssh: Umožňuje přenos přes SSH.
-  -delete: Smaže soubory v cílovém umístění, které nejsou ve zdrojovém.

## Příklady použití Rsync

### 1. Základní kopírování souborů a složek

Synchronizace adresáře „data“ z místního do jiného adresáře na stejném disku:

```bash
rsync -avh /domaci/data/ /domaci/zaloha/data/
```

### 2. Kopírování přes SSH na vzdálený server

Přenese obsah adresáře „data“ na vzdálený server s IP adresou 192.168.1.10:
```bash
rsync -avh -e ssh /domaci/data/ uzivatel@192.168.1.10:/domaci/zaloha/data/
```

### 3. Kopírování a mazání souborů, které již nejsou ve zdroji

Kopírování s možností smazání všech souborů v cíli, které nejsou ve zdroji:

```bash
rsync -avh --delete /domaci/data/ /domaci/zaloha/data/
```

## Jednoduchý zálohovací skript s Rsync

Tento skript provede zálohu složky /home/uzivatel/data do složky /backup/data. Stačí zkopírovat a upravit cesty podle potřeby.

1. Vytvoř nový skript:
```bash
nano ~/zaloha.sh
```

2. Vlož následující kód:

```bash
#!/bin/bash

# Nastavení cesty ke zdroji a cíli
ZDROJ="/home/uzivatel/data/"
CIL="/backup/data/"

# Spuštění rsync s potřebnými volbami
rsync -avh --delete "$ZDROJ" "$CIL"

# Výpis zprávy o úspěchu
echo "Záloha dokončena: $(date)"
```

3. Skript ulož a ukonči editor.

4. Nastav spustitelný příznak skriptu

```bash
chmod +x ~/zaloha.sh
```
5. Skript spusť:

```bash
./zaloha.sh
```

Skript provede synchronizaci mezi složkami a vypíše potvrzení o dokončení s aktuálním časem.

## Obnova dat pomocí Rsync

Před obnovou se ujisti, že máš správnou cestu ke zdroji (místo, kde máš zálohu) a cíl (místo, kam chceš soubory obnovit).

### Příklad obnovy lokálních souborů

Pokud záloha existuje v adresáři `/backup/data/` a chceš obnovit soubory do `/home/uzivatel/data/`, použij následující příkaz:

```bash
rsync -avh /backup/data/ /home/uzivatel/data/
```
### Obnova s možností mazání nepotřebných souborů

Pokud chceš obnovit data a zároveň odstranit soubory v cílové složce, které nejsou ve zdrojové složce (používá se při obnově na původní stav), přidej volbu --delete:

```bash
rsync -avh --delete /backup/data/ /home/uzivatel/data/
```

### Obnova ze vzdáleného serveru

Pokud je záloha na vzdáleném serveru, obnovu můžeš provést podobně, přidáním `-e ssh` a zadáním vzdálené adresy:

```bash
rsync -avh -e ssh uzivatel@192.168.1.10:/backup/data/ /home/uzivatel/data/
```

## Automatizace záloh pomocí Cron

1. Otevři cron editor:

```bash
crontab -e
```

2. Přidej řádek:

```bash
0 2 * * * /home/uzivatel/zaloha.sh
```
Tento příkaz zajistí, že se záloha spustí každý den ve 2:00.