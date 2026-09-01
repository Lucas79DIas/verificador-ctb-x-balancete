# Verificador CTB x Balancete

Ferramenta web (arquivo único, sem backend) para conciliar saldos de contas financeiras entre o CTB e o Balancete (SICAP-DC).

## O que ela faz

Para cada **conta financeira + fonte de recurso**, compara:

- **CEC 1**: saldo final do CTB (registro `20`, saldo CEC = 1) x soma do saldo final no Balancete das contas contábeis iniciadas em `1.1.1`, **exceto** `1.1.1.1.1.01.00`, `1.1.1.1.1.02.00`, `1.1.1.2.1.01.00` e todas as iniciadas em `1.1.1.3`.
- **CEC 3**: saldo final do CTB (registro `20`, saldo CEC = 3) x soma do saldo final no Balancete das contas contábeis iniciadas em `1113`.

O relatório final lista só as divergências, com conta financeira, fonte, saldo CTB, saldo balancete e diferença — e pode ser exportado em PDF (usa a impressão nativa do navegador).

## Como usar

Abra o `index.html` no navegador (local ou publicado via GitHub Pages / Vercel), suba o ZIP do AM (contém `CTB.CSV`) e o ZIP do Balancete (contém `BALANCETE.CSV`), e clique em "Verificar". Todo o processamento roda no navegador — nenhum arquivo é enviado para servidor.

## Regras de leitura dos arquivos

**CTB.CSV**, linhas `20`:
```
registro;orgao;contaFinanceira;fonte;saldoCEC;saldoInicial;saldoFinal
```

**BALANCETE.CSV**, linhas `17`:
```
registro;contaContabil;complementoConta;atributoFinanceiro;contaFinanceira;fonte;CO;saldoInicial;naturezaSaldo;debitoMes;creditoMes;saldoFinal;naturezaFinal
```

O campo `CO` é ignorado no acumulado por conta financeira + fonte. Valores negativos no CTB equivalem à natureza de crédito no balancete; positivos, à natureza de débito.
