# utl-renamimg-coordinated-lists-of-of-column-names
Renamimg coordinated lists of of column names
    Renaming coordinated lists of column names                                                               
                                                                                                             
    github                                                                                                   
    https://tinyurl.com/qrmpxzo                                                                              
    https://github.com/rogerjdeangelis/utl-renamimg-coordinated-lists-of-of-column-names                     
                                                                                                             
    This helps when merging tables with the same names in a datastep.                                        
    Lets you easily use column position instead of column name.                                              
                                                                                                             
    Handles these cases                                                                                      
                                                                                                             
        rename = (a b c = f1-f3)                                                                             
        rename = (f1-f3 = a b c)                                                                             
        rename = (a b c = x y x)                                                                             
                                                                                                             
    BOGUS EXAMPLE TO SHOW RENAMING                                                                           
    (simple OLDNAME= NEWNAME on input and NEWNAME=OLDNAME on output)                                         
                                                                                                             
    Mutiply two tables with the same column names using datastep language.                                   
    I do realize R, IML, 'proc score' and perhaps 'proc cor' can do this but                                 
    renaming coordinated lists has many applications.                                                        
                                                                                                             
    macros                                                                                                   
    https://tinyurl.com/y9nfugth                                                                             
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories               
                                                                                                             
    Answers are easy. A good question and example are hard?                                                  
                                                                                                             
    *_                   _                                                                                   
    (_)_ __  _ __  _   _| |_                                                                                 
    | | '_ \| '_ \| | | | __|                                                                                
    | | | | | |_) | |_| | |_                                                                                 
    |_|_| |_| .__/ \__,_|\__|                                                                                
            |_|                                                                                              
    ;                                                                                                        
                                                                                                             
    data have1 have2;                                                                                        
                                                                                                             
     call streaminit(4321);                                                                                  
                                                                                                             
     array alphas[26] A B C D E F G H I J K L M N O P Q R S T U V W X Y Z;                                   
                                                                                                             
     do lyn = 1 to 5;                                                                                        
                                                                                                             
        do ltr=1 to 26;                                                                                      
           alphas[ltr] = RAND("Bernoulli", .25) +1 ;  /* 1s with .25 probability */                          
        end;                                                                                                 
                                                                                                             
        output have1;                                                                                        
                                                                                                             
        do ltr=1 to 26;                                                                                      
           alphas[ltr] = int(4*RAND("Uniform")) + 1;                                                         
        end;                                                                                                 
                                                                                                             
        output have2;                                                                                        
     end;                                                                                                    
     drop ltr lyn ;                                                                                          
     stop;                                                                                                   
                                                                                                             
    run;quit;                                                                                                
                                                                                                             
    NOTE SAME NAMES                                                                                          
                                                                                                             
    HAVE1 total obs=5                                                                                        
                                                                                                             
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z                                                     
                                                                                                             
     1 1 1 2 2 1 1 1 1 1 1 2 1 2 2 1 1 1 2 2 1 1 1 1 1 1                                                     
     1 1 1 2 1 1 2 1 2 1 2 2 1 2 1 1 1 1 2 1 1 1 2 1 1 1                                                     
     1 1 1 1 1 1 2 1 2 1 1 1 1 1 2 2 1 1 1 1 1 1 2 2 2 1                                                     
     1 1 2 1 1 1 1 1 2 1 1 1 1 1 1 1 2 2 1 2 1 1 1 1 1 1                                                     
     1 2 1 1 1 1 1 2 2 2 1 1 1 1 1 1 2 1 2 2 2 1 1 1 1 1                                                     
                                                                                                             
                                                                                                             
    HAVE2 total obs=5                                                                                        
                                                                                                             
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z                                                     
                                                                                                             
     3 2 2 4 4 3 1 2 1 3 4 2 4 1 2 4 4 4 4 4 3 2 3 1 2 1                                                     
     4 3 2 1 2 1 2 1 2 3 3 3 4 1 2 3 4 4 4 1 4 2 2 4 4 2                                                     
     4 3 3 3 4 1 3 3 2 3 4 4 4 1 4 1 2 3 3 1 1 1 1 1 1 3                                                     
     1 3 3 2 4 2 2 4 2 3 1 3 4 1 1 4 4 1 1 3 1 2 3 4 4 3                                                     
     1 2 1 2 1 3 1 2 2 4 2 3 1 1 4 3 1 4 4 4 3 2 2 3 1 1                                                     
                                                                                                             
    *            _               _                                                                           
      ___  _   _| |_ _ __  _   _| |_                                                                         
     / _ \| | | | __| '_ \| | | | __|                                                                        
    | (_) | |_| | |_| |_) | |_| | |_                                                                         
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                        
                    |_|                                                                                      
    ;                                                                                                        
    PRODUCT OF HAVE1 AND HAVE2                                                                               
                                                          | RULES                                            
    WORK.WANT total obs=5                                 |              Product                             
                                                          | HAVE1  HAVE2  WANT                               
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z  |  Z       Z     Z                                 
                                                          |                                                  
     3 2 2 8 8 3 1 2 1 3 4 4 4 2 4 4 4 4 8 8 3 2 3 1 2 1  |  1       1     1                                 
     4 3 2 2 2 1 4 1 4 3 6 6 4 2 2 3 4 4 8 1 4 2 4 4 4 2  |  1       2     2                                 
     4 3 3 3 4 1 6 3 4 3 4 4 4 1 8 2 2 3 3 1 1 1 2 2 2 3  |  1       3     3                                 
     1 3 6 2 4 2 2 4 4 3 1 3 4 1 1 4 8 2 1 6 1 2 3 4 4 3  |  1       3     3                                 
     1 4 1 2 1 3 1 4 4 8 2 3 1 1 4 3 2 4 8 8 6 2 2 3 1 1  |  1       1     1                                 
                                                                                                             
                                                                                                             
    *          _       _   _                                                                                 
     ___  ___ | |_   _| |_(_) ___  _ __                                                                      
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                     
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                    
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                    
                                                                                                             
    ;                                                                                                        
                                                                                                             
    %utlnopts;                      /* not needed it just supresses a lengthy log */                         
                                                                                                             
    proc datasets lib=work nolist;  /* for ruruns */                                                         
       delete want;                                                                                          
    run;quit;                                                                                                
                                                                                                             
    %symdel _vars _oldn _newn;    /* for ruruns */                                                           
                                                                                                             
    %let _vars=%utl_varlist(have1);                                                                          
                                                                                                             
    %array(_old,values=&_vars);       %put &_old1 &_old26 &_oldn;  * A Z 26;                                 
    %array(_new,values=f1-f&_oldn);   %put &_new1 &_new26 &_newn;  * f1 f26 26;                              
                                                                                                             
                                                                                                             
                                    /*  new names = old names */                                             
    data mrg(rename=(%do_over(_new _old,phrase=%str(?_new = ?_old)))) ;                                      
                                                                                                             
      merge have1                   /*  old names =new names */                                              
            have2(rename=(%do_over(_old _new,phrase=%str(?_old=?_new))));                                    
                                                                                                             
      array old &_vars;                                                                                      
      array new f1-f&_newn;                                                                                  
                                                                                                             
      do idx=1 to &_oldn;                                                                                    
        new[idx] = new[idx]*old[idx];                                                                        
      end;                                                                                                   
                                                                                                             
      keep f1-f&_newn;                                                                                       
      put 'AFTER ' old[1]=  new[1]=;                                                                         
    run;quit;                                                                                                
                                                                                                             
    %utlopts; /* turn log back on */                                                                         
                                                                                                             
      *_              _                                                   
    | |_ ___   ___ | |___                                               
    | __/ _ \ / _ \| / __|                                              
    | || (_) | (_) | \__ \                                              
     \__\___/ \___/|_|___/                                              
                                                                        
    ;                                                                   
                                                                        
    * CLEAN UP GENERATED ARRAYS;                                        
    * also in many macros;                                              
                                                                        
    %deletemacarray(_old);                                              
    %deletemacarray(_new);                                              
                                                                        
    %macro deleteMacArray(arr,start_index);                             
      %local J;                                                         
      %do J = 1 %to &&&arr.n;                                           
        %put *&&&arr.&J.*;                                              
        %symdel &arr.&J. / NOWARN;                                      
      %end;                                                             
      %symdel &arr.n / nowarn;                                          
    %mend deleteMa                                                      
                                                                        
    * IF YOU WANT THE CODE GENERATED BY DO_OVER;                        
                                                                        
    %utlnopts;                                                          
    data;put %do_over(_new _old,phrase=%str("?_new  = ?_old" /));       
    data;put %do_over(_new _old,phrase=%str("?_old= = ?_new" /));       
    ;run;quit;                                                          
    %utlopts;                                                           
                                                                        
                                                                        
    f1  = A                                                             
    f2  = B                                                             
    f3  = C                                                             
    f4  = D                                                             
    f5  = E                                                             
    f6  = F                                                             
    f7  = G                                                             
    f8  = H                                                             
    f9  = I                                                             
    f10  = J                                                            
    f11  = K                                                            
    f12  = L                                                            
    f13  = M                                                            
    f14  = N                                                            
    f15  = O                                                            
    f16  = P                                                            
    f17  = Q                                                            
    f18  = R                                                            
    f19  = S                                                            
    f20  = T                                                            
    f21  = U                                                            
    f22  = V                                                            
    f23  = W                                                            
    f24  = X                                                            
    f25  = Y                                                            
    f26  = Z                                                            
                                                                        
    A= = f1                                                             
    B= = f2                                                             
    C= = f3                                                             
    D= = f4                                                             
    E= = f5                                                             
    F= = f6                                                             
    G= = f7                                                             
    H= = f8                                                             
    I= = f9                                                             
    J= = f10                                                            
    K= = f11                                                            
    L= = f12                                                            
    M= = f13                                                            
    N= = f14                                                            
    O= = f15                                                            
    P= = f16                                                            
    Q= = f17                                                            
    R= = f18                                                            
    S= = f19                                                            
    T= = f20                                                            
    U= = f21                                                            
    V= = f22                                                            
    W= = f23                                                            
    X= = f24                                                            
    Y= = f25                                                            
    Z= = f26                                                            
                                                                        
