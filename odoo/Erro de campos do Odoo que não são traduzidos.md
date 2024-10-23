#odoo 

Erro de campos do Odoo que não são traduzidos e não aparecem no arquivo de tradução:

Os campos da model 'service.contract.line' do mudulo 'service_contract_line_event' não estavam sendo traduzidos porque eles foram declarados no modulo 'service_contract_management' e posteriormente movidos para 'service_contract_line_event'.

Todo campo declarado no Odoo possui um id externo (igual ao que ocorre com as views xml). Na tabela 'ir_model_data' pode se verificar esses ids externos de cada campo. O erro acontece porque após movermos o campo para outro modulo, o registro dele em 'ir_model_data' não é atualizado, e continua indicando o modulo antigo como o modulo onde o campo esta sendo declarado. Por esse motivo, quando geramos os arquivos de tradução, os campos não estão presentes no arquivo .po para serem traduzidos. O Odoo acha que os campos pertencem a outro modulo e não os insere no arquivo de tradução e nem carrega sua tradução, se a mesma estiver presente.

O erro acontece apenas nas bases em modulo de contrato foi instalado antes dessa separação de módulos (base da multidados). As bases mais novas já identificam o modulo onde os campos são declarados corretamente.

Isso foi resolvido apenas por cadastro, através do query SQL (em anexo) e carregando a tradução dos módulos em questão.

```sql
SELECT id, module,name FROM ir_model_data WHERE module = 'service_contract_management' and res_id in (SELECT id from ir_model_fields where model_id in (SELECT id from ir_model where name = 'service.contract.line'))

UPDATE ir_model_data set module = 'service_contract_line_event' where id in (SELECT id FROM ir_model_data WHERE module = 'service_contract_management' and res_id in (SELECT id from ir_model_fields where model_id in (SELECT id from ir_model where name = 'service.contract.line')))

```