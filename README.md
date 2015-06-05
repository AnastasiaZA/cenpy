CenPy
=======

An interface to explore and query the US Census API and return Pandas
Dataframes. Ideally, this package is intended for exploratory data analysis
and draws inspiration from sqlalchemy-like interfaces and `acs.R`. 

Usage
------

Pop `cenpy` into your `PYTHONPATH`. Then, import the module or the submodules.
Once done, importing `cenpy` will provide the `explorer` and `base` modules. To
create a connection:

```
cxn = cenpy.base.Connection('2010sf1')
```

Check the variables required and geographies supported:

```
cxn.variables #is a pandas dataframe containing query-able vbls
cxn.geographies #is a pandas dataframe containing query-able geographies
```

Note that some geographies (like tract) have higher-level requirements that
you'll have to specify for the query to work.

The structure of the query function maps to the Census API's use of `get`,
`for`, and `in`. The main arguments for the query function are `cols`,
`geo_unit` and `geo_filter`, and map backwards to those predicates,
respectively. If more predicates are required for the search, they can be added
as keyword arguments at the end of the query. 

The `cols` argument must be a list of columns to retrieve from the dataset.
Then, you must specify the `geo_unit` and `geo_filter`, which provide *what*
the unit of aggregation should be and *where* the units should be. `geo_unit`
must be a string containing the unit of analysis and an identifier. For
instance, if you want all counties in Arizona, you specify `geo_unit = 'county:*'`
and `geo_filter` = {'state','04'}. 

ToDo:
------

- [ ] Provide Joins to geodata the TIGER files REST api
- [ ] Provide more conveneince functions, like lookups for place and state
abbreviations to state fips/gnis codes.
