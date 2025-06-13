For editing/updating/deleting **one2many** and **many2many** please refer below syntaxes :

* `(0, 0, { values })` link to a new record that needs to be created with the given values dictionary
* `(1, ID, { values })` update the linked record with `id = ID` (write values on it)
* `(2, ID)` remove and delete the linked record with `id = ID` (calls unlink on ID, that will delete the object completely, and the link to it as well)
* `(3, ID)` cut the link to the linked record with `id = ID` (delete the relationship between the two objects but does not delete the target object itself)
* `(4, ID)` link to existing record with `id = ID` (adds a relationship)
* `(5)` unlink all (like using `(3,ID)` for all linked records)
* `(6, 0, [IDs])` replace the list of linked IDs (like using `(5)` then `(4,ID)` for each ID in the list of IDs)

Original post [here](https://www-odoo-com.translate.goog/forum/help-1/how-to-fill-many2many-or-many2one-fields-while-creating-a-record-in-another-model-128503?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt-BR&_x_tr_pto=sc)
