# fibonacci

#!/usr/bin/env bash
# fib.sh - print the first n Fibonacci numbers (starting from 0, 1)

set -euo pipefail
IFS=$'\n\t'

usage() {
  echo "Usage: $0 n  # prints first n Fibonacci numbers (n >= 1)"
  exit 2
}

# require exactly one argument
if [ "$#" -ne 1 ]; then
  usage
fi

n=$1

# validate that n is a positive integer
if ! [[ "$n" =~ ^[0-9]+$ ]] || [ "$n" -lt 1 ]; then
  echo "Error: n must be a positive integer" >&2
  usage
fi

a=0
b=1
count=0

# loop n times, each iteration outputs the current 'a' then advances the pair (a,b)
while [ "$count" -lt "$n" ]; do
  printf '%d\n' "$a"
  tmp=$(( a + b ))
  a=$b
  b=$tmp
  count=$(( count + 1 ))
done
