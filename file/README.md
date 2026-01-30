services:
  cor-0:
    container_name: cor-0
    image: offchainlabs/nitro-node:v3.9.4-7f582c3
    user: 0:0
    restart: unless-stopped
    stop_grace_period: 5m
    command:
      --chain.id=18964747554
      --chain.name=COR-0
      --parent-chain.connection.url=https://sepolia-arb-rpc.agnc.my.id
      --chain.info-json="[{\"chain-id\":18964747554,\"parent-chain-id\":421614,\"parent-chain-is-arbitrum\":true,\"chain-name\":\"COR-0\",\"chain-config\":{\"chainId\":18964747554,\"homesteadBlock\":0,\"daoForkBlock\":null,\"daoForkSupport\":true,\"eip150Block\":0,\"eip150Hash\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"eip155Block\":0,\"eip158Block\":0,\"byzantiumBlock\":0,\"constantinopleBlock\":0,\"petersburgBlock\":0,\"istanbulBlock\":0,\"muirGlacierBlock\":0,\"berlinBlock\":0,\"londonBlock\":0,\"clique\":{\"period\":0,\"epoch\":0},\"arbitrum\":{\"EnableArbOS\":true,\"AllowDebugPrecompiles\":false,\"DataAvailabilityCommittee\":true,\"InitialArbOSVersion\":40,\"InitialChainOwner\":\"0xD6b9d395c3368B5412b3a7D2fb0D7327a83Ed792\",\"GenesisBlockNum\":0,\"MaxCodeSize\":24576,\"MaxInitCodeSize\":49152}},\"rollup\":{\"bridge\":\"0x974d0762eBD0883411A75de8BF41a4c7eA93c03d\",\"inbox\":\"0x08a6C4Bbf77A2387D7DDAD41Fd55193467B6e2b6\",\"sequencer-inbox\":\"0xeeF64Fe40F04aB1aB55016A242D4C278721237FD\",\"rollup\":\"0x39F772DfF00756bec951b691778f58d10a753a57\",\"validator-wallet-creator\":\"0x2c37dCBCE3fbe32c9Ba62892F1E41DbB023BB62b\",\"stake-token\":\"0x980B62Da83eFf3D4576C647993b0c1D7faf17c73\",\"deployed-at\":229017936}}]"
      --node.feed.input.url=wss://feed.testnet1a.cortensor.org
      --execution.forwarding-target=https://sequencer.testnet1a.cortensor.org
      --node.data-availability.enable
      --node.data-availability.rest-aggregator.enable
      --node.data-availability.rest-aggregator.online-url-list=https://testnet1a-das-servers.cortensor.org
      --http.api=net,web3,eth,debug
      --http.corsdomain=*
      --http.addr=0.0.0.0
      --http.vhosts=*
      --http.port=10001
      --ws.addr=0.0.0.0
      --ws.port=10002
      --ws.origins=*
    volumes:
      - ./rpc-data:/root/.arbitrum
    ports:
      - 10001:10001 # JSON-RPC endpoint
      - 10002:10002 # WebSocket endpoint
    networks:
      - cnid

networks:
  cnid:
    external: true
