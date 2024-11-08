# Průvodce AUR a Instalace Správců Balíčků (yay a paru)

## Co je AUR?

AUR (Arch User Repository) je komunitní repozitář pro Arch Linux. Nabízí tisíce balíčků, které nejsou dostupné v oficiálním repozitáři Archu. Tyto balíčky vytvářejí uživatelé komunity, což umožňuje sdílet software, který ještě není oficiálně podporován. AUR obsahuje PKGBUILD skripty, které automatizují sestavení a instalaci balíčků ze zdrojových kódů.

### Výhody AUR
- **Široký výběr softwaru** – Obsahuje software, který nemusí být oficiálně dostupný.
- **Komunitní podpora** – Uživatelé mohou přidávat, upravovat a diskutovat o balíčcích.
- **Automatizovaná kompilace** – Pomocí PKGBUILD je možné jednoduše sestavit a nainstalovat balíčky.

## Instalace `yay` a `paru`

Pro snadné používání AUR je nejlepší mít nainstalovaný správce balíčků, jako je `yay` nebo `paru`. Oba umožňují vyhledávání, instalaci a aktualizaci balíčků přímo z AUR.

### Instalace `yay`

1. Nejprve aktualizujte systém:

 ```bash
 sudo pacman -Syu
```

2. Nainstalujte potřebné balíčky:

```bash
sudo pacman -S --needed git base-devel
```

3. Naklonujte repozitář yay:

```bash
git clone https://aur.archlinux.org/yay.git
```

4. Přepněte se do složky yay a nainstalujte:

```bash
cd yay
makepkg -si
```

5. Yay je nyní nainstalován! Můžete ho použít k instalaci balíčků z AUR.

### Instalace paru

1. Pokud již máte systém aktualizovaný, naklonujte repozitář paru:

```bash
git clone https://aur.archlinux.org/paru.git
```
2. Přepněte se do složky `paru` a nainstalujte:

```bash
cd paru
makepkg -si
```

Paru je nyní připraven k použití pro instalaci balíčků z AUR.

## Základní příkazy pro yay a paru

Jakmile máte `yay` nebo `paru` nainstalované, můžete začít spravovat balíčky z AUR. Níže jsou základní příkazy:

### Instalace balíčků

```bash
yay -S <název_balíčku>
paru -S <název_balíčku>
```

Tyto příkazy stáhnou, zkompilují a nainstalují balíček.

### Aktualizace všech balíčků včetně AUR

```bash
yay -Syu
paru -Syu
```

Aktualizuje všechny balíčky včetně těch z AUR.

### Odinstalace balíčku

```bash
yay -R <název_balíčku>
paru -R <název_balíčku>
```

Odstraní balíček z vašeho systému.

### Vyhledávání balíčku

```bash
yay -Ss <název_balíčku>
paru -Ss <název_balíčku>
```

Umožňuje prohledávat AUR i oficiální repozitáře.

### Vyčištění cache

Po aktualizacích můžete chtít vyčistit staré balíčky z cache.

```bash
yay -Sc
paru -Sc
```

Tímto odstraníte staré balíčky, což může uvolnit místo na disku.
