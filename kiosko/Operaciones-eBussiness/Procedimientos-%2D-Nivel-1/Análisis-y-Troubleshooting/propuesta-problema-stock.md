
> en base a un incidente se solicita crear una mejora carga de stock producto kiosko desde la bodega **10485** 

>referencia incidente y requerimiento
#1256 
#1094


| RESPONSABLE | NOMBRE |
|--|--|
|Dev | @<CE92F1CF-CC80-4918-A8EB-AE517BE1F894>|
| Scrum | @<84DD55FC-9653-62DD-928B-C4621D644C72>   |
| Arch| @<04B7645A-ABF7-63AB-896E-9C6134EE014C>   |
| AWS | @<BA5D6A33-7C77-651A-ABE8-4E6164958123>   |
| Ops | @<EEDB8383-0602-601E-80FC-A3F939D4073B>    |


::: mermaid
 sequenceDiagram
    %%autonumber
    participant pmm as pmm
    participant back as back-end process
    participant ops as manual/crontab  <br/> << option >>
    participant sftp as aws sftp/s3
    participant ld as lambda
    participant db as redis
    participant log as cloudwatch 
    participant kiosk as kiosko

    back->>pmm: scheduled plsql cd 10485
    pmm-->>back: convert to csv file
    opt manual
     ops->>back : browse search archive 10485    
     back-->>ops: get day's files 10485
    end

    opt scheduled
     back->>sftp: get day's files 10485
    end

    ops->>sftp: add files 10485   

    %%rect rgb(138, 98, 0)
    
    sftp->>ld: S3 event notifications
    ld->>sftp: browse search archive 10485
    sftp-->>ld: get day's files 10485
    loop for each row file
      alt this valid
          ld ->> db: insert/update row stock
      else error format
          ld ->> log: format error/skip header
      end
    end
    ld ->> log: processed vs total quadrature       
     alt successful
        ld ->> sftp:move to processed folder
     else failed file
        ld ->> sftp:move to error folder
     end
    kiosk->>db: get stock by product
    db-->>kiosk: get stock by product 
    %%end
:::
