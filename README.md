# utl-first-non-missing-value-carried-backwords-FVCB
First non missing value carried backwords FVCB 
    Thanks, Mark                                                                                                       
                                                                                                                       
    Replacing GitHub                                                                                                   
                                                                                                                       
       First non missing value carried backwords by group                                                              
                                                                                                                       
         Solution by                                                                                                   
             Keintz, Mark                                                                                              
             Handles 'by group processing'                                                                             
             mkeintz@wharton.upenn.edu                                                                                 
                                                                                                                       
             SAS-L                                                                                                     
             https://listserv.uga.edu/cgi-bin/wa?A2=SAS-L;b73b5fc2.2009a                                               
                                                                                                                       
    GitHub                                                                                                             
    https://tinyurl.com/y357nw64                                                                                       
    https://github.com/rogerjdeangelis/utl-first-non-missing-value-carried-backwords-FVCB                              
                                                                                                                       
    stackoverflow                                                                                                      
    https://tinyurl.com/y5re4j38                                                                                       
    https://stackoverflow.com/questions/63560423/missing-value-of-column-based-on-date-comparison-sql                  
                                                                                                                       
    Intelligence is the ability and curiosity to formulate questions.                                                  
                                                                                                                       
    Thanks user31735                                                                                                   
    https://stackoverflow.com/users/3861199/user31735                                                                  
    /*                   _                                                                                             
    (_)_ __  _ __  _   _| |_                                                                                           
    | | `_ \| `_ \| | | | __|                                                                                          
    | | | | | |_) | |_| | |_                                                                                           
    |_|_| |_| .__/ \__,_|\__|                                                                                          
            |_|                                                                                                        
    */                                                                                                                 
                                                                                                                       
    /*                                                                                                                 
    Having said: "Of course this code would need modification if you have                                              
    data sorted by ID/DATE and some id's end with a missing rate.  You need                                            
    a way to avoid bringing a "future" value back from another id. "                                                   
                                                                                                                       
    Not much change is needed - just the "until" condition and an added BY statement:                                  
    */                                                                                                                 
                                                                                                                       
    data have;                                                                                                         
    input id DATE :date9. RATE;                                                                                        
    format date date9.;                                                                                                
    datalines;                                                                                                         
    101 31DEC2014 .                                                                                                    
    101 31DEC2015 .                                                                                                    
    101 31DEC2016 .                                                                                                    
    101 31DEC2017 0.1600                                                                                               
    101 31DEC2018 0.1700                                                                                               
    101 31DEC2019 0.1770                                                                                               
    101 31DEC2020 .                                                                                                    
                                                                                                                       
    102 31JAN2014 .                                                                                                    
    102 31JAN2015 .                                                                                                    
    102 31JAN2016 .                                                                                                    
    102 31JAN2017 0.2600                                                                                               
    102 31JAN2018 0.2700                                                                                               
    102 31JAN2019 0.2770                                                                                               
    102 31DEC2020 .                                                                                                    
    run;                                                                                                               
                                                                                                                       
                                                                                                                       
    HAVE total obs=14                                                                                                  
                                | RULES                                                                                
      ID      DATE        RATE  | RATE                                                                                 
                                |                                                                                      
     101    31DEC2014     .     | 0.160                                                                                
     101    31DEC2015     .     | 0.160                                                                                
     101    31DEC2016     .     | 0.160                                                                                
     101    31DEC2017    0.160  | 0.160  ** 0.160 was carried backward                                                 
     101    31DEC2018    0.170  |                                                                                      
     101    31DEC2019    0.177  |                                                                                      
     101    31DEC2020     .     | ====> do not reach into the next by group for non-                                   
                                |                                                                                      
     102    31JAN2014     .     |  | 0.260                                                                             
     102    31JAN2015     .     |  | 0.260                                                                             
     102    31JAN2016     .     |  | 0.260                                                                             
     102    31JAN2017    0.260  |  | 0.260 ** 0.260 was carried backward                                               
     102    31JAN2018    0.270  |  | 0.270                                                                             
     102    31JAN2019    0.277  |  | 0.277                                                                             
     102    31DEC2020     .     |                                                                                      
                                                                                                                       
    /*           _               _                                                                                     
      ___  _   _| |_ _ __  _   _| |_                                                                                   
     / _ \| | | | __| `_ \| | | | __|                                                                                  
    | (_) | |_| | |_| |_) | |_| | |_                                                                                   
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                  
                    |_|                                                                                                
    */                                                                                                                 
                                                                                                                       
    WANT total obs=14                                                                                                  
                                                                                                                       
      ID      DATE      RATE                                                                                           
                                                                                                                       
     101    31DEC2014  0.160                                                                                           
     101    31DEC2015  0.160                                                                                           
     101    31DEC2016  0.160                                                                                           
     101    31DEC2017  0.160                                                                                           
     101    31DEC2018  0.170                                                                                           
     101    31DEC2019  0.177                                                                                           
     101    31DEC2020   .                                                                                              
     102    31JAN2014  0.260                                                                                           
     102    31JAN2015  0.260                                                                                           
     102    31JAN2016  0.260                                                                                           
     102    31JAN2017  0.260                                                                                           
     102    31JAN2018  0.270                                                                                           
     102    31JAN2019  0.277                                                                                           
     102    31DEC2020   .                                                                                              
                                                                                                                       
    /*                                                                                                                 
     _ __  _ __ ___   ___ ___  ___ ___                                                                                 
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                
    | .__/|_|  \___/ \___\___||___/___/                                                                                
    |_|                                                                                                                
    */                                                                                                                 
                                                                                                                       
    data want;                                                                                                         
      do _n_=1 by 1 until (rate or last.id);                                                                           
        set have;                                                                                                      
        by id;                                                                                                         
      end;                                                                                                             
      do _n_=1 to _n_;                                                                                                 
        set have (drop=rate);                                                                                          
        output;                                                                                                        
      end;                                                                                                             
    run;quit;                                                                                                          
                                                                                                                       
                                                                                                                       
                                                                                                      
                                                                                                                         
                                                                                                                         
                                                                                                                         
                                                                                                                         
