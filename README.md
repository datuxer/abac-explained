# abac-explained
Personal thoughts on a Attribute Based Access Control sys. Don't worry, not quite ABAC.

(a naive explanation for myself during learning these things)

As usual, when not coding I'm trying to write down my thoughts on a subject.
 
## Motivation 
 
 Used ACL and RBAC, both nice stuff, I'm feeling sometimes that I have unwanted constraints and repetitive wor, and sometime that I have to hardcode a lot and I will love to have something really simple and more generic, that can be used in any scenario.
 
 Instead of normal hardcoded attribute sets, I'll try to find a way to use more generic attributes.
 
## Links
 
http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf
http://www.axiomatics.com/attribute-based-access-control.html
http://profsandhu.com/dissert/Dissertation_Xin_Jin.pdf

## Definitions

Not going to follow exactly the standards or papers, but some definitions are needed for a common language:
 - `U` = user/subject, the person that authenticate in the sys
 - `UA` = user attributes that count in the process
 - `O` = object (named in some places "resource"), any data record
 - `OT` = object type, more generic than `O`
 - `OA` = object attributes that count in the process
 <!--- `E` = environment/scope-->
 <!--- `EA` = environment attributes-->
 - `P` = policy
 - `PA` = policy attributes, maybe to be renamed after I'll find the right definition below
 - `R` = rule
 - `Ac` = action/activity, including read, write, edit, delete, copy, execute, and modify (a CRUD+)  
  
I will use only those, but I have to keep in mind that any other type of attributes can be added.

## Attributes (`A`)

 We can look at `UA` and `OA` as metadata of the subject.

 For a user attributes can be department, region, its organization level, probably a role
 
 For an object is certainly the `OT`, technically can be associated with a table in SQL or a collection in NoSQL.
 Other can be defined.
 
  `any` = a special attribute that means we don't care about the attribute :) 
 
## Policy (`P`)
 
 `P` is the way to define access rights. There are several point of view how to define it, I will concentrate over one of them.
 
 `P` is first defined as a match for `UA`, each `P` must be unique defined by its `PA` set. 
 Missing attributes means `any`. That will deliver some issues when adding new `UA`, probably the bes approach is to find the best and most restricted set.

 ```
 ...
 [
    "department",
    "region",
    "role"
 ]
 ...
 ```

 `P` contains the list of all accessible `OT` named `R`. Each `Ac` can contain any of the `UA` plus `own` and `any`
   
 ```
 ...
 [
    { 
        res: "docs",
        C: true,
        R: "region",
        U: "department",
        D: "own"
    }
 ]
 ...
 ```
 
 
 