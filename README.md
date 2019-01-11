#  Rod Cutting Problem

### Requirenments
You have rodes with the same length and you have also a list with cutting lengths. 

### Problem
How to assign the cuts in order to minimize the number of rods?

### Solution
```{python}

def calulate_assignments(row_length, cuts, unit):
    
    # Problem initialization
    assignments = []
    wastage = 0
    row_id = 1
    residual = row_length
    
    #Sort the cut lengths in descending order
    cuts = sorted(cuts, reverse=True)

    while cuts != []:
        for cutting_id, cutting in enumerate(cuts):
            
            go_to_next_row=True
            
            # When a cut is valid do assignment!
            if cutting <= residual:
                cuts.pop(cutting_id)
                residual = residual - cutting
                assignments.append({'Rod id': row_id, 'Cut length':str(cutting) +' '+ unit})
                go_to_next_row=False

        # Go to the next row!        
        if go_to_next_row or residual == 0:
            row_id +=1
            assignments.append('') # Trick for illustration purposes in print :-)
            wastage = wastage + residual
            residual = row_length
   
        if cuts == []:
            wastage = wastage + residual
            
    print('*'*60)
    print('RESULTS')
    print('*'*60)
    
    print('-'*10 + 'Assignments' + '-'*10)
    for assignment in assignments:
        print(assignment)
    
    print('-'*9 + 'Number of Rodes' + '-'*9)
    print(row_id)
    
    print('-'*12 + 'Wastage' + '-'*12)
    print(wastage, unit)
    
    print('*'*60)

```

### Example
```
row_length = 10
cuttting_list = [10,1,7,9,3,1,1,8]

calulate_assignments(row_length=row_length,
                     cuts=cuttting_list, 
                     unit='m'
                    )
```

**Results**

***************************************
RESULTS
***************************************

----------Assignments----------

{'Rod id': 1, 'Cut length': '10 m'}


{'Rod id': 2, 'Cut length': '9 m'}
{'Rob id': 2, 'Cut length': '1 m'}


{'Rod id': 3, 'Cut length': '8 m'}
{'Rod id': 3, 'Cut length': '1 m'}
{'Rod id': 3, 'Cut length': '1 m'}


{'Rod id': 4, 'Cut length': '7 m'}
{'Rod id': 4, 'Cut length': '3 m'}


---------Number of Rodes---------

5

------------Wastage------------

10 m
***************************************
