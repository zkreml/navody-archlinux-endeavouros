# Řešení chyb s klíči v Arch Linux a EndeavourOS

Pokud při aktualizaci nebo instalaci dostáváte chyby jako “Nelze aktualizovat: podpis od *** má nedostatečnou důvěru” nebo “neplatný či poškozený balíček”, postupujte následovně pro řešení.


## 1. Aktualizace klíčů pro podepisování balíčků

Pro zajištění správného ověření balíčků je potřeba aktualizovat klíče pro Arch Linux i EndeavourOS.

Uživatelé **EndeavourOS** by měli použít následující příkaz pro aktualizaci obou klíčových balíčků:

```bash
sudo pacman -Sy archlinux-keyring endeavouros-keyring
```

Pokud používáte čistý `Arch Linux,` stačí aktualizovat pouze archlinux-keyring:

```bash
sudo pacman -Sy archlinux-keyring
```
⚠️ **Tip**: Zkontrolujte, že je systémový čas správně nastavený, protože nesprávný čas může způsobit problémy s klíči.

## 2. Kontrola a odstranění poškozených balíčků

Je možné, že balíček je skutečně poškozený. V takovém případě ho odstraňte z cache, aby si pacman stáhl novou verzi:

```bash
sudo rm /var/cache/pacman/pkg/nazev_balicku.pkg.tar.zst
```

Pokud není konkrétní balíček zmíněn, může být příčinou neúplné stažení. Odstraňte částečné soubory stažení pomocí:

```bash
sudo rm /var/cache/pacman/pkg/*.part
```
## 3. Vyčištění pacman keyring a obnovení klíčů

V případě přetrvávajících problémů můžete vymazat pacman keyring a vytvořit nový:

```bash
sudo mv /etc/pacman.d/gnupg /root/pacman-key.bak
sudo pacman-key --init
sudo pacman-key --populate archlinux endeavouros
sudo pacman -Syy archlinux-keyring endeavouros-keyring
sudo pacman -Syyu
```

## Opětovná instalace klíčů

Pokud stále nemáte úspěch a jste si jisti, že balíčky jsou v pořádku, můžete provést nucenou instalaci klíčů z cache:

```bash
sudo pacman -U /var/cache/pacman/pkg/{archlinux,endeavouros}-keyring*.pkg.tar.zst
```

Po této operaci znovu zkuste příkaz pro aktualizaci.

## 5. Instalace AUR balíčků s PGP klíči

Při instalaci balíčku z AUR může být vyžadován PGP klíč k ověření souborů. Pokud klíč není importován, zobrazí se chyba podobná této:

```bash
llvm-5.0.0.src.tar.xz ... CHYBA (neznámý veřejný klíč 0FC3042E345AD05D)
libcxx-5.0.0.src.tar.xz ... CHYBA (neznámý veřejný klíč 0FC3042E345AD05D)
```

Pro vyřešení jednoduše importujte chybějící klíč do svého keyringu:

```bash
gpg --recv-key 0FC3042E345AD05D
```

Po provedení tohoto kroku by instalace měla pokračovat bez dalších potíží.
