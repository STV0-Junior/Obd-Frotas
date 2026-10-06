# Lógica de cálculos e alertas

Esta pasta é destinada às regras que interpretam leituras do veículo, identificam condições que merecem atenção e ajudam a planejar manutenção preventiva.

## Estado atual

As regras ainda não estão implementadas nesta pasta. Os indicadores e exemplos do dashboard são dados de demonstração; não constituem um diagnóstico nem uma previsão calculada a partir de um veículo conectado.

## Como a análise deve funcionar

1. Receber leituras identificadas com unidade, horário e origem (ECU, sensor ou entrada manual).
2. Verificar se a leitura é válida e se o veículo ou adaptador oferece esse parâmetro.
3. Comparar o valor com limites apropriados ao veículo, às condições de uso e ao procedimento do fabricante.
4. Considerar duração, repetição e tendência antes de emitir um alerta, evitando reagir a uma leitura isolada ou inválida.
5. Exibir o sinal observado, sua gravidade e uma recomendação de verificação, sem afirmar uma causa que os dados não comprovem.

## Exemplos de regras futuras

| Sinal observado | Possível alerta interno | Cuidados de interpretação |
| --- | --- | --- |
| Temperatura do líquido de arrefecimento acima da faixa especificada por tempo relevante | `COOLANT_TEMP_HIGH` | Validar a leitura da ECU e o limite adequado ao veículo. Se a ECU informar o DTC P0217, preservar esse código e sua descrição; não inventar um código OBD para uma regra própria. |
| Tensão da bateria persistentemente baixa nas condições de medição adequadas ou tendência anormal | `BATTERY_VOLTAGE_LOW` | Uma única leitura não confirma bateria defeituosa. Considerar motor ligado/desligado, estado de carga, partida e dados disponíveis do sistema de bateria. |
| Pressão abaixo da referência de uma roda | `TIRE_PRESSURE_LOW` | Requer leitura TPMS compatível ou medição informada. Nem todo adaptador OBD-II fornece pressão dos pneus. Identificar a roda e usar a pressão recomendada para o veículo; não criar um DTC OBD genérico. |
| Combustível abaixo do nível definido para aviso | `FUEL_LEVEL_LOW` | O nível pode não estar disponível no adaptador e pode variar com o movimento do veículo. É um aviso de abastecimento, não necessariamente uma falha mecânica. |

Os identificadores da coluna são nomes internos sugeridos para alertas do aplicativo, não códigos de falha OBD-II. Quando a ECU fornecer um DTC real, guardar e apresentar o código original, sem substituí-lo por uma regra própria.

## Prevenção sem promessas indevidas

Uma regra pode avisar que um sinal está fora da faixa ou que uma tendência merece inspeção. Para estimar falha futura com confiança, serão necessários histórico suficiente, parâmetros confiáveis e validação em veículos reais. O sistema deve informar incerteza, evitar recomendações perigosas e deixar claro que alertas não substituem inspeção profissional.

## Testes esperados

- Cobrir valores normais, acima e abaixo do limite e valores ausentes ou inválidos.
- Testar leituras transitórias para verificar se a persistência evita falsos alarmes.
- Testar diferentes unidades e limites específicos por veículo.
- Manter exemplos de dados simulados separados de dados obtidos em veículo conectado.