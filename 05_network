# Useful function for network information finding

function ipsort {
    sort -t . -k 1,1n -k 2,2n -k 3,3n -k 4,4n
}

function strip_proto {
    echo $1 | sed -E -e "s~(https?|ftp|ssh|rsync){0,1}://~~" -e "s~/.*~~"
}

function host {
    local host=$(strip_proto $1)
    shift

    command host "${host}" "$@"
}

function dig {
    local host=$(strip_proto $1)
    shift

    command dig "${host}" "$@"
}

function nslookup {
    local host=$(strip_proto $1)
    shift

    command nslookup "${host}" "$@"
}

function ipwhois {
    local host=$(strip_proto $1)

    if [[ $host =~ [0-9]{1,3}\.[0-9]{1,3}\. ]]; then
        local ip=$host
    else
        # Assuming this is a dns name
        local ip=$(dig +short $host)
    fi

    if [[ -z "${ip}" ]]; then
        return 1;
    fi

    echo "IP whois for ${ip}"
    command whois "${ip}" "$@"
}

# Taken from: https://github.com/twe4ked/dotfiles/blob/master/shell/functions/ping.sh
# Modified to pull out strip_proto func and improve proto list
function ping {
    local host=$(strip_proto $1)
    shift

    command ping "$host" "$@"
}

function whois {
    local host=$(strip_proto $1)
    shift

    command whois "$host" "$@"
}
