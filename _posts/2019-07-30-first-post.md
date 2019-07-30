---
title: "Study about Quicksork"
date: 2019-07-30 
categories: Algorithm
---

To the record,

Definition 
"Quicksork" is one of functions to make arrangement a given number array. Usually, people use this function to make ascending order.

Okay, Let's start with the code

there is a code. And I'm going to split this code and explain every part.

---
#include <stdio.h>
#define LEN 9

/*PART.1*/  
void quick_sort(int num[],int start, int end);
void tracer(int num[],int len);

/*PART.3*/ 
void quick_sort(int num[],int start, int end)
{
    int i,j,p;
    int tempValue; 
    if (start < end) 
    {
        i = start+1; 
        j = end;
        p = num[start]; 
        do 
        {
            while (num[i] < p)
            {
                i++; 
            };
            while (num[j] > p) 
            {
                j--; 
            }
            if (i < j)
            {
                tempValue = num[j];
                num[j] = num[i];
                num[i] = tempValue;
            }
        } while (i < j);
        num[start] = num[j];
        num[j] = p;
        printf("[start Index: %d, end Index: %d, Pivot: %d]\n",start,end,p); 
        tracer(num,LEN); 
        quick_sort(num,start,j-1);
        quick_sort(num,j+1,end);
    }
}
  
void tracer(int num[],int len)
{
    int i;
    for(i=0;i<len;i++)
    {
        printf("%d\t",num[i]);
    }
    printf("\n\n");
}

/*PART.2*/ 
int main(void)
{    
    int testArr[] = {485,241,454,325,452,685,498,890,281};
    quick_sort(testArr, 0, LEN-1); 
}
---

PART1.
#include <stdio.h>
#define LEN 9
  
void quick_sort(int num[],int start, int end);
void tracer(int num[],int len);
  
[In this part, define the function we will use. Quicksork fucntion is main function that arrange the numbers in a given array, and tracer is a helper function which help to see what happen in our code.]


PART2.
int main(void)
{    
    int testArr[] = {485,241,454,325,452,685,498,890,281};
    quick_sort(testArr, 0, LEN-1); 
}

[This part is main. We create an arbitrary test_arry, and give this array to quicksort algorithm. Important feature of Quicksort function is Recursion. Until array meets the given conditions, the array go around a set loop. Here, the given condition means arrangement of numbers in array.]


PART3.
void quick_sort(int num[],int start, int end)
{
    int i,j,p;
    int tempValue; 
    if (start < end) 
    {
        i = start+1; 
        j = end;
        p = num[start]; 
        do 
        {
            while (num[i] < p)
            {
                i++; 
            };
            while (num[j] > p) 
            {
                j--; 
            }
            if (i < j)
            {
                tempValue = num[j];
                num[j] = num[i];
                num[i] = tempValue;
            }
        } while (i < j);
        num[start] = num[j];
        num[j] = p;
        printf("[start Index: %d, end Index: %d, Pivot: %d]\n",start,end,p); 
        tracer(num,LEN); 
        quick_sort(num,start,j-1);
        quick_sort(num,j+1,end);
    }
}
  
void tracer(int num[],int len)
{
    int i;
    for(i=0;i<len;i++)
    {
        printf("%d\t",num[i]);
    }
    printf("\n\n");
}

[In this part, honestly, I recommend to write down array, i, j, p(pivot) with following the sequence of function. and there is not nesseceary comment to understand. Check your writing and my writing.]

First quicksort loop
         'p'
Array = {485,     241,     454,     325,     452,     685,     498,     890,     281}
i=1   ->                                              i=5
j=8   ->                                                                         j=8       swap
        {485,     241,     454,     325,     452,     281,     498,     890,     685}  
        

         'p'
Array = {485,     241,     454,     325,     452,     281,     498,     890,     685}
i=5   ->                                                       i=6  
j=8   ->                                                                j=7                swap
        {485,     241,     454,     325,     452,     281,     890,     498,     685}
        
         'p'
Array = {485,     241,     454,     325,     452,     281,     890,     498,     685}
i=6   ->                                                       i=6  
j=7   ->                                              j=5                                  
                                                       .
                                            Escape do-while loop 
                                    (can't meet the condition "if (i < j)")
                                                      'p'                                           
        {281,     241,     454,     325,     452,     485,     890,     498,     685}      pivot swap

Second quicksort loop(1)--left side of pivot(right after first quicksort)
         'p'
Array = {281,     241,     454,     325,     452}        
i=1   ->                   i=2
j=4   ->          j=1                              
                            .
                 Escape do-while loop 
         (can't meet the condition "if (i < j)")
                  'p'
        {241,     281,     454,     325,     452}   pivot swap
       (--completed--)  

                           'p'
Array =                   {454,     325,     452}
i=1   ->                                           i=3
j=4   ->                                     j=2    
                            Escape do-while loop
                                             'p'
                          {452,     325,     454}   pivot swap

                           'p'
Array =                   {454,     325}
i=1   ->                                  i=2
j=4   ->                            j=1
                        Escape do-while loop
                                    'p'
                          {325,     452}   pivot swap


Result -> {241,     281,     325,     452,     454}



                                                    Second quicksort loop(2)--right side of pivot(right after first quicksort)
                                                               'p'
                                                      Array = {890,     498,     685}        
                                                      i=1   ->                         i=3
                                                      j=4   ->                   j=2                              
                                                                Escape do-while loop
                                                                                 'p'
                                                              {685,     498,     890}   pivot swap
                                                              
                                                               'p'
                                                      Array = {685,     498}        
                                                      i=1   ->                i=2
                                                      j=4   ->          j=1
                                                            Escape do-while loop
                                                                        'p'
                                                              {498,     685}   pivot swap
                                                              
                                                    Result -> {498,     685,     890}
                                                              
                                                              
                                                          
                                                          
                                                          
Consequently, we can get the result as this array.
              
              {241,     281,     325,     452,     454,     498,     685,     890}
              
                                                                                                       


                                                                                                                 
                                                                                              




 

