# Tarea

ransferir_capitales(origen, destino, monto)
transferir_deuda(origan, destino, monto)
transferir_divisas(origen, destino, monto)
transferir_efectivo(origen, destino, monto)

## Pregunta I

> Ulises con cuenta en GBM compra a Julieta con cuenta en Santander 400 títulos de AMZ (Amazon) a 66048.20 MXM pagaderos con cash.

```
start transaction;
transferir_capitales("GBM_ulises","Santander_julieta",400);

if success then
  commit;
  transferir_efectivo("Santander_julieta","GBM_Ulises",66048.20);

if error then
  rollback;
```

## Pregunta II

> Sebas Dulong con cuenta en Citi vende a Javier Orcazas 1200 títulos de GME (GameStop) a 3714.88 pagaderos 100 títulos de deuda gubernamental con valor de 2998.12 y el restante con cash

```
cash_settlement = 3714.99 - 2998.12;

start transaction;
transferir_capitales("Citi_sebas-dulong","Banco_jav-orcazas",1200);

if success then
  
  start transaction;
  transferir_deuda("Banco_jav-orcazas","Citi_sebas-dulong",100);
  
  if success then
    commit;
    commit;
    transferir_efectivo("Banco_jav-orcazas","Citi_sebas-dulong",cash_settlement);
  
  if error then
    rollback;
if error then
  rollback;
```

## Pregunta III

> DJ Delgado con cuenta en Scotia vende 20000 USD a un exchange rate de 25.2 MXN y 300 títulos de deuda corporativa a un precio de 40032.71 a Frida Kaori con cuenta en Inbursa pagaderos enteramente con cash.

```
cash_settlement_forex = 20000*25.2;
cash_settlement_corp-bond = 40032.71

start transaction;

transferir_divisas("Scotia_dj-delgado","Inbursa_frida-vodkaori",20000);

if success then
  commit;
  transferir_efectivo("Inbursa_frida-vodkaori","Scotia_dj-delgado",cash_settlement_forex);
if error then
  rollback;

start transaction;
transferir_deuda("Scotia_dj-delgado","Inbursa_frida-vodkaori",300);

if success then
  commit;
  transferir_efectivo("Inbursa_frida-vodkaori","Scotia_dj-delgado",cash_settlement_corp-bond);
  
if error then
  rollback;

```
