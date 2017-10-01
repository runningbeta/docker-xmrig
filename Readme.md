# runningbeta/xmrig

This is an Alpine Linux Docker image running [XMRig miner](https://github.com/xmrig/xmrig).

The goal of this project is to quickly enable you to mine Monero without the hassle of knowing how to install or secure your mining software.

Using an [Alpine Linux](https://www.alpinelinux.org/) container you get a very lightweight image ~4MB and the benefit of Alpine Linux's security model.
Image is configured to run the miner as a dedicated restricted user.

# Basic example

`docker run --restart unless-stopped --read-only -m 50M -c 512 runningbeta/xmrig -o POOL -u WALLET -p PASSWORD -k`

# Failover

`docker run --restart unless-stopped --read-only -m 50M -c 512 runningbeta/xmrig -o POOL01 -o POOL02 -u WALLET -p PASSWORD -k`

# Full example

`docker run --restart unless-stopped --read-only -m 50M -c 512 runningbeta/xmrig -o r8.network:5222 -o pool.supportxmr.com:5555 -u 4AjqdPQxRA1aot1nwAFn8M6wHcUhZupiJMjAkbxeitGV4YBZsn4rKBYdUEHQC5GxTwP8tg8yhuHoYL2qCEcTxeRN4vr47ae -p x -k`

# Options

## Docker Arguments
`--restart unless-stopped`

If the miner crashes we want the docker service to restart it.

`--read-only`

This image does not need rw access.
If there are bug/exploits in the pool/software you are a little more protected.

`-m 50M`

Restricts memory usage to 50MB.

`-c 512`

By default XMRig will use <= half of your cores. Setting a relevant share count will protect you from a runaway process locking your system.

## XMRig Arguments
`--help`

All standard XMRig arguments are supported, using `--help` will list all of them.
```bash
# docker run runningbeta/xmrig --help
```
`-t`

When manually setting threads with `-t` you need to configure the correct CPU shares for docker.

IE if you have 4 cores each core is worth 256 `( 1024 / 4 )` and so to use 3 threads, CPU shares will need to be set to 756.
```bash
# docker run -c 756 runningbeta/xmrig ... -t 3
```

# Donations

Development of Monero and tools can be supported directly through donations.

Default donation 5% (5 minutes in 100 minutes) can be reduced to 1% via command line option --donate-level. Currently all auto-donations are to the open source [XMRig Github project](https://github.com/xmrig/xmrig). Future updates may change this. Until then you can make an one time donation to this organizations:

monero-project XMR: `44AFFq5kSiGBoZ4NMDwYtN18obc8AemS33DBLWs3H7otXft3XjrpDtQGv7SqSsaBYBb98uNbr2VBBEt7f2wfn3RVGQBEP3A`
xmrig XMR: `48edfHu7V9Z84YzzMa6fUueoELZ9ZRXq9VetWzYGzKt52XU5xvqgzYnDK9URnRoJMk1j8nLwEVsaSWJ4fhdUyZijBGUicoD`
r8-network XMR: `4AjqdPQxRA1aot1nwAFn8M6wHcUhZupiJMjAkbxeitGV4YBZsn4rKBYdUEHQC5GxTwP8tg8yhuHoYL2qCEcTxeRN4vr47ae`
