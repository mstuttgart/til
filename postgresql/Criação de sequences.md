Em alguns casos do odoo (principalmente modulo de temas), pode ser necessário criar sequences diretamente no postgresql


```sql
-- SEQUENCE: public.theme_ir_ui_view_id_seq (nome da sequence a ser criada)

DROP SEQUENCE IF EXISTS public.theme_ir_ui_view_id_seq; -- nome da sequence

CREATE SEQUENCE IF NOT EXISTS public.theme_ir_ui_view_id_seq
    INCREMENT 1  
    START 1  
    MINVALUE 1  
    MAXVALUE 9223372036854775807  
    CACHE 1  
    OWNED BY theme_ir_ui_view.id; -- nome da tabela

ALTER SEQUENCE public.theme_ir_ui_view_id_seq  
    OWNER TO "multierp12"; -- nome do usuario
```