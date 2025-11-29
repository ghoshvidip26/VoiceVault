# VoiceVault

## Deployment Notes

- The package uses the named address `VoiceVault` (`0x0bf154dc582a43ec543711fba16c44e02cec2f660868f1fa164f1816fa7f1952`) defined in `Move.toml` and the module namespace `VoiceVault::voice_identity` so the compiled modules are owned by that account.
- `aptos move deploy-object` built a resource object at `0xb1b87a60d1206943e4676cc0aef0f45a4e16580620697e06bf6e28e11ac841fb`, which became the transaction sender; Aptos rejects publishing when the module address (0x0bf1...) does not match the sender, hence the repeated `MODULE_ADDRESS_DOES_NOT_MATCH_SENDER` simulation failure.
- Switching to `aptos move publish --sender-account 0x0bf154dc582a43ec543711fba16c44e02cec2f660868f1fa164f1816fa7f1952` publishes directly from the named address, aligning the compiled module address with the sender and succeeding (`tx 0xf89aec8857860ad91136f8d6b7627b36bd5f17a8c9ddd9ee53bf5074af84a6be`).

## Next Steps

1. Continue adding modules and entry points under `VoiceVault::voice_identity`, keeping all named addresses consistent with the account used for publishing.
2. When deploying to a resource account instead, add that account’s address to `Move.toml` (e.g., `VoiceVault = 0xb1b8…`) or pass it via `--named-addresses` so the module address matches the sender.
3. Monitor the transaction hash on the Aptos testnet explorer to confirm execution and gas usage as you iterate.
