merkletree
=====

A library for creating and manipulating [Merkle Trees](https://en.wikipedia.org/wiki/Merkle_tree).

Build
-----

    $ rebar3 compile

Usage
-----

```erlang
1> T1 = merkletree:build([{<<"k1">>, <<"v1">>}, {<<"k2">>, <<"v2">>}]).
{inner,undefined,
       <<47,117,74,159,119,66,45,125,235,249,102,242,254,162,44,
         50,133,42,101,138,119,227,132,31,217,113,...>>,
       1,<<"k1">>,<<"k2">>,
       {inner,<<"k1">>,
              <<66,1,101,13,125,236,26,190,129,40,42,92,87,173,238,12,
                232,158,232,...>>,
              0,<<"k1">>,<<"k1">>,nil,nil},
       {inner,<<"k2">>,
              <<78,154,73,127,252,215,113,136,242,141,110,48,76,105,140,
                31,17,4,...>>,
              0,<<"k2">>,<<"k2">>,nil,nil}}
2> T2 = merkletree:build([{<<"k1">>, <<"v1">>}, {<<"k3">>, <<"v3">>}, {<<"k2">>, <<"v2">>}]).
{inner,undefined,
       <<90,184,45,234,57,190,164,245,46,225,97,89,211,124,149,
         115,0,201,73,146,176,19,22,154,35,62,...>>,
       2,<<"k1">>,<<"k3">>,
       {inner,undefined,
              <<47,117,74,159,119,66,45,125,235,249,102,242,254,162,44,
                50,133,42,101,...>>,
              1,<<"k1">>,<<"k2">>,
              {inner,<<"k1">>,
                     <<66,1,101,13,125,236,26,190,129,40,42,92,...>>,
                     0,<<"k1">>,<<"k1">>,nil,nil},
              {inner,<<"k2">>,
                     <<78,154,73,127,252,215,113,136,242,141,110,...>>,
                     0,<<"k2">>,<<"k2">>,nil,nil}},
       {inner,<<"k3">>,
              <<153,101,135,160,120,152,149,38,91,132,203,189,7,154,63,
                37,55,207,...>>,
              0,<<"k3">>,<<"k3">>,nil,nil}}
3> merkletree:diff(T1, T2).
[<<"k3">>]
4> merkletree:keys(T2).
[<<"k1">>,<<"k2">>,<<"k3">>]
```
