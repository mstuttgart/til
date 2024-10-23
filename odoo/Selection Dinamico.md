```python

    def _journal_dest_id(self):
        """ Metodo para montar dinamicamente o filtro dos Diários
        """
        domain = [
            ('company_id', '=', self.env.user.company_id.id),
            ('type', 'in', ('bank', 'cash')),
        ]
        journal_ids = self.env['account.journal'].sudo().search(domain, order="name") # noqa

        return list(map(lambda journal: (str(journal.id), ', '.join([journal.name, journal.company_id.name])), journal_ids)) # noqa


    journal_dest_id = fields.Selection(
        selection=lambda self: self._journal_dest_id(),
        string="Journal",
        help="Destination Journal.",
        required=False,
    )
```