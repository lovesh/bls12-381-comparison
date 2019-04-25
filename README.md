# bls12-381-comparison
This is a quick benchmark between [Apache Milagro](https://github.com/apache/incubator-milagro-crypto) and
ZCash's [Pairing](https://crates.io/crates/pairing) library for the BLS signature scheme

The BLS signature scheme is useful for creating aggregated signatures. I wanted to find out which pairing library would be faster.
Any comments or suggestions to my quick and dirty test here are welcome. I'm not sure if I implemented according to each
libraries intended use but this is how I was able to get it to work.

To run the tests run the following command
```rust
cargo run --release -- --iterations {integer}
```

On average as of April 9 2019, ZCash's pairing tends to run 2-4X slower.   
The performance difference comes from the cost of hashing the message. In the Apache Milagro implementation, 
the messages is hashed using Blake and the result is multiplied by the generator to get a point. This is insecure and can be seen [here](https://github.com/zcash-hackworks/bn/pull/2#discussion_r111367525).
