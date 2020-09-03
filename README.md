# utl-first-non-missing-value-carried-backwords-FVCB
First non missing value carried backwords FVCB 
    First non missing value carried backwords FVCB                                                                       
                                                                                                                         
    github                                                                                                               
    https://tinyurl.com/y357nw64                                                                                         
    https://github.com/rogerjdeangelis/utl-first-non-missing-value-carried-backwords-FVCB                                
                                                                                                                         
    Ingeneous algorithm by User31735                                                                                     
         https://stackoverflow.com/users/3861199/user31735                                                               
                                                                                                                         
    stackoverflow                                                                                                        
    https://tinyurl.com/y5re4j38                                                                                         
    https://stackoverflow.com/questions/63560423/missing-value-of-column-based-on-date-comparison-sql                    
                                                                                                                         
                                                                                                                         
    /*                   _                                                                                               
    (_)_ __  _ __  _   _| |_                                                                                             
    | | `_ \| `_ \| | | | __|                                                                                            
    | | | | | |_) | |_| | |_                                                                                             
    |_|_| |_| .__/ \__,_|\__|                                                                                            
            |_|                                                                                                          
    */                                                                                                                   
    options missing='.';                                                                                                 
    data have;                                                                                                           
     input DATE$ RATE;                                                                                                   
    cards4;                                                                                                              
    31DEC2014 .                                                                                                          
    31DEC2015 .                                                                                                          
    31DEC2016 .                                                                                                          
    31DEC2017 0.1600                                                                                                     
    31DEC2018 0.1700                                                                                                     
    31DEC2019 0.1770                                                                                                     
    31JAN2014 .                                                                                                          
    31JAN2015 .                                                                                                          
    31JAN2016 .                                                                                                          
    31JAN2017 0.2600                                                                                                     
    31JAN2018 0.2700                                                                                                     
    31JAN2019 0.2770                                                                                                     
    ;;;;                                                                                                                 
    run;quit;                                                                                                            
                                                                                                                         
    WORK.HAVE total obs=12                                                                                               
                           | RULES                                                                                       
       DATE       RATE     | RATE                                                                                        
                           |                                                                                             
     31DEC201     .        | 0.160                                                                                       
     31DEC201     .        | 0.160                                                                                       
     31DEC201     .        | 0.160                                                                                       
     31DEC201    0.160     | 0.160  ** 0.160 was carried backward                                                        
     31DEC201    0.170     | 0.170                                                                                       
     31DEC201    0.177     | 0.177                                                                                       
                                                                                                                         
     31JAN201     .        | 0.260                                                                                       
     31JAN201     .        | 0.260                                                                                       
     31JAN201     .        | 0.260                                                                                       
     31JAN201    0.260     | 0.260                                                                                       
     31JAN201    0.270     | 0.270                                                                                       
     31JAN201    0.277     | 0.277                                                                                       
                                                                                                                         
    /*           _               _                                                                                       
      ___  _   _| |_ _ __  _   _| |_                                                                                     
     / _ \| | | | __| `_ \| | | | __|                                                                                    
    | (_) | |_| | |_| |_) | |_| | |_                                                                                     
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                    
                    |_|                                                                                                  
    */                                                                                                                   
                                                                                                                         
     WORK.WANT total obs=12                                                                                              
                                                                                                                         
                                                                                                                         
       RATE      DATE                                                                                                    
                                                                                                                         
      0.160    31DEC201                                                                                                  
      0.160    31DEC201                                                                                                  
      0.160    31DEC201                                                                                                  
      0.160    31DEC201                                                                                                  
      0.170    31DEC201                                                                                                  
      0.177    31DEC201                                                                                                  
      0.260    31JAN201                                                                                                  
      0.260    31JAN201                                                                                                  
      0.260    31JAN201                                                                                                  
      0.260    31JAN201                                                                                                  
      0.270    31JAN201                                                                                                  
      0.277    31JAN201                                                                                                  
                                                                                                                         
    /*                                                                                                                   
     _ __  _ __ ___   ___ ___  ___ ___                                                                                   
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                  
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                  
    | .__/|_|  \___/ \___\___||___/___/                                                                                  
    |_|                                                                                                                  
    */                                                                                                                   
                                                                                                                         
    data want(drop=r);                                                                                                   
       do _n_=1 by 1 until (rate);   * do until non missing rate;                                                        
          set have;                                                                                                      
          r = rate;  * keep the non missing;                                                                             
       end;                                                                                                              
       do _n_=1 to _n_;                                                                                                  
          set have;                                                                                                      
          rate=r;                                                                                                        
          output;                                                                                                        
       end;                                                                                                              
    run;quit;                                                                                                            
                                                                                                                         
                                                                                                                         
                                                                                                                         
                                                                                                                         
