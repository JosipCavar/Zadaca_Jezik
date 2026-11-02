# Alan Ford + Ollama

Python skripta za osnovnu obradu teksta (brojanje znakova, traženje podteksta, dijeljenje po separatoru) povezana s lokalnim LLM-om preko [Ollame](https://ollama.com). Primjer koristi tekst stripa *Alan Ford: Grupa TNT*, ali radi s bilo kojom `.txt` datotekom.

## Što radi

**Obrada teksta**
- `read_file`, `len_file`: čitanje datoteke i broj znakova
- `count_chars`: ukupan broj pojavljivanja zadanih znakova
- `pos_subtext`, `count_subtext`: pozicije i broj pojavljivanja podteksta (uključujući preklapajuća)
- `split_text`, `sep_text`: dijeljenje teksta po separatoru

**Ollama**
- `ask_ollama`: šalje upit lokalnom modelu
- `summarize_text`: sažima dugačak tekst po dijelovima
- `ask_about_text`: pitanje o cijelom tekstu
- `ask_about_keyword`: izdvoji okolinu zadane riječi i pita model samo o tome

## Zahtjevi

- Python 3.8+
- [Ollama](https://ollama.com) instalirana i pokrenuta
- Python paket `ollama`

## Instalacija

```bash
git clone https://github.com/<korisnik>/<repozitorij>.git
cd <repozitorij>

pip install ollama
ollama pull llama3.1
```

## Pokretanje

1. Stavite svoju tekstualnu datoteku u isti folder i postavite njezin naziv u `FILENAME` na vrhu skripte.
2. Provjerite da Ollama radi (`ollama serve`).
3. Pokrenite:

```bash
python alan_ford_ollama.py
```

Skripta će ispisati početak teksta, pokrenuti testove te zatim sažetak i odgovor na primjer pitanja od modela.

## Primjer korištenja u kodu

```python
from alan_ford_ollama import read_file, ask_about_keyword

tekst = read_file('moja_datoteka.txt')
print(ask_about_keyword(tekst, 'New York', 'Što se događa u ovim ulomcima?'))
```

## Postavke

| Postavka | Gdje | Opis |
|----------|------|------|
| `MODEL` | vrh skripte | Ollama model (npr. `llama3.1`, `qwen2.5`) |
| `FILENAME` | vrh skripte | putanja do ulazne datoteke |
| `num_ctx` | `ask_ollama` | veličina konteksta; povećajte za dulje tekstove |

## Napomene

- Ollamin zadani kontekst je malen, zato skripta eksplicitno postavlja `num_ctx`.
- Za bolje rezultate na hrvatskom probajte veće modele.
- Testovi u `run_tests()` očekuju točno određenu datoteku (broj znakova, pozicije). S drugom datotekom neki testovi će prikazati `X`, što je očekivano.

## Licenca

Dodajte licencu po želji (npr. MIT).
