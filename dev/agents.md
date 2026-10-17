# Együttműködési irányelvek

## Hatókör

Ez a repó a DevMac Guardian macOS-ellenőrzőt tartalmazza. A monitorozás legyen helyi, adatminimalizált és alapértelmezetten csak olvasható.

## Kötelező szabályok

1. Titok, token, jelszó, privát kulcs, böngészési előzmény és teljes rendszer- vagy alkalmazásnapló nem kerülhet commitba.
2. A rendszeres `check` futás nem módosíthat hálózatot, szolgáltatást, felhasználói adatot vagy alkalmazásbeállítást.
3. Javítás csak külön parancsban, előnézettel, szűk engedélylistával és idempotens művelettel készülhet.
4. Törlés, force-kill, VPN-/tűzfal-átállítás és külső adatküldés nem adható hozzá kifejezett felhasználói engedély nélkül.
5. Új ellenőrzéshez determinisztikus teszt és világos, azonosítható finding ID szükséges.
6. A jelentés bizonyítékot közölhet, de érzékeny értéket nem. Környezeti változó teljes tartalmát tilos naplózni.
7. A CI minimális GitHub-jogosultságot használjon; a repó privát maradjon.

## Ellenőrzés változtatás előtt

```bash
PYTHONPATH=src python3 -m pytest -q
python3 tools/policy_check.py
PYTHONPATH=src python3 -m compileall -q src tests tools
```

Minden PR írja le a mérhető viselkedésváltozást, a visszaállítás módját és a friss tesztbizonyítékot.
