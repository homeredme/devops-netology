1. 
```
c = "a+b" - указали текст а не переменные
d = "1+2" - значения переменных, так как по умолчанию это строки 
e = "3"   - за счет скобок выполненяется сложение 
```

2.  В условии не хватет закрывающей скобки, нет задержки
    
    Как вариант:
```    
    while (( 1 == 1 ))
    do
        curl https://localhost:4757
        if (($? != 0))
        then
            date >> curl.log
        fi
        sleep 5
    done
```

3. 
```
    hosts="192.168.0.1 173.194.222.113 87.250.250.242"
    for h in $hosts
    do
        for i in {1..5}
        do
    	    curl --connect-timeout 2 -Is $h:80 > /dev/null
            case $? in
                0)
                    result=successful
                    ;;
                *)
                    result=error
                    ;;
            esac              
            echo "$(date)    check $h result=$result" >> log
        done
    done
```    

4.
```
    hosts="192.168.0.1 173.194.222.113 87.250.250.242"
    result=0
    for h in $hosts
    do
        for i in {1..5}
        do
    	    curl --connect-timeout 2 -Is $h:80 > /dev/null
            result=$?
            if [ $result -ne 0 ]; then     
                echo "$(date)    check $h result=error" >> error
                break
            fi
        done 
        if [ $result -ne 0 ]; then     
            break
        fi       
    done
```   