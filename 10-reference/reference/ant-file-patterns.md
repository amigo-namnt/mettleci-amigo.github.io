# Ant File Patterns

A number of MettleCI Commands use [Ant file pattens](https://ant.apache.org/manual/dirtasks.html#patterns) for the specification of files upon which they operate. For example, the `remote upload` ([link](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/716603405/Remote+Upload+Command)) and `remote download` ([link](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/716636187/Remote+Download+Command)) commands use Ant patterns to specify which files will be included in the command’s transfer process. For example, to *shallow* copy all files in the `unittest` directory use the pattern `unittest/*`.  For recursive (deep) copying of the same directory use `unittest/**/*`. 

Ant is also powerful enough to do more complex matching such as all XML files within an arbitrarily-deep directory tree (i.e., `unittest/**/*.xml`) or to shallow copy all XML files only a single directory deep within the `unittest` directory, i.e., `unittest/*/*.xml`) (noting this time the *single* `/*/`).

Multiple transfer patterns can be supplied using a comma separated notation. For example, `unittest/**/*.xml,unittest/**/*.csv` matches all XML and CSV files within an arbitrarily-deep directory tree. It should be noted that many of the MettleCI commands supporting the use of Ant syntax also support the use of multiple `-pattern` parameters, so in the previous example it may be more readable to use a command of the form…

```
$> mettleci namespace command \
   -patern unittest/**/*.xml \
   -pattern unittest/**/*.csv   
```

## MettleCI Components using ANT Patterns

*   Page:
    
    [Remote Download Command](/wiki/spaces/MCIDOC/pages/716636187/Remote+Download+Command)
    
*   Page:
    
    [Remote Upload Command](/wiki/spaces/MCIDOC/pages/716603405/Remote+Upload+Command)
    
*   Page:
    
    [ISX Set-Params Command](/wiki/spaces/MCIDOC/pages/458850355/ISX+Set-Params+Command)