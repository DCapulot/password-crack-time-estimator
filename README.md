# password-crack-time-estimator

Estimador educacional do tempo necessário para "quebrar" uma senha por força bruta offline, com base no tamanho do alfabeto usado (minúsculas, maiúsculas, números, símbolos) e em diferentes cenários de poder de processamento.

## Motivação

Este projeto nasceu a partir de um vídeo sobre ataques de força bruta offline contra hashes de senha vazados. A proposta aqui é puramente matemática e didática: calcular, com base em entropia e espaço de busca, quanto tempo um ataque desse tipo levaria — sem executar nenhum ataque real.

## O que o script faz

- Recebe uma senha digitada pelo usuário (fica só na memória local, nunca é salva ou enviada).
- Identifica quais tipos de caractere ela usa (minúsculas, maiúsculas, números, símbolos, espaços).
- Calcula o espaço de busca total (todas as combinações possíveis) e a entropia em bits.
- Classifica a força da senha (muito fraca → muito forte).
- Estima o tempo de quebra em diferentes cenários de ataque:
  - Tentativa manual/online
  - CPU doméstica com hash rápido sem proteção
  - GPU única com hash rápido (ex.: MD5/SHA1 sem salt)
  - Cluster de GPUs
  - Hash bem protegido (bcrypt/Argon2)

## Como usar

```bash
python tempo_quebra_senha.py
```

O programa vai pedir a senha e o cenário de ataque, e devolver o tempo estimado (médio e pior caso) para descobri-la.

## Testando na prática (opcional)

Para comparar a estimativa teórica com um teste real, é possível:

1. Criar um hash de uma senha escolhida por você mesmo (ex.: com `hashlib` em Python).
2. Usar uma ferramenta como **hashcat** ou **John the Ripper** para tentar quebrar esse hash criado por você.
3. Comparar o tempo real gasto pela ferramenta com o tempo estimado por este script.

Esse fluxo reproduz o cenário de "hash vazado + ataque offline" sem envolver contas, sistemas operacionais ou dispositivos reais de terceiros.

## Aviso

Este projeto é apenas para fins educacionais, para entender por que senhas curtas ou previsíveis são fracas. Não deve ser usado para tentar acessar contas, sistemas ou dispositivos sem autorização.

## Licença

Uso livre para fins de estudo.
