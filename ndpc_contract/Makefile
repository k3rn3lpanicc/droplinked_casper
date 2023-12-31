prepare:
	rustup target add wasm32-unknown-unknown

build-contract:
	cd contract && cargo build --release --target wasm32-unknown-unknown
	wasm-strip contract/target/wasm32-unknown-unknown/release/contract.wasm 2>/dev/null | true
	cp contract/target/wasm32-unknown-unknown/release/contract.wasm deploy/contract.wasm
	cp deploy/contract.wasm /home/k3rn3lpanic/Desktop/casper_demo_backend/casper_wallet/casper_wallet/src/contract.wasm
	
build-session:
	cd session && cargo build --release --target wasm32-unknown-unknown
	wasm-strip session/target/wasm32-unknown-unknown/release/contract.wasm 2>/dev/null | true
	cp session/target/wasm32-unknown-unknown/release/contract.wasm deploy/session.wasm

build-payment:
	cd payment && cargo build --release --target wasm32-unknown-unknown
	wasm-strip payment/target/wasm32-unknown-unknown/release/contract.wasm 2>/dev/null | true
	cp payment/target/wasm32-unknown-unknown/release/contract.wasm deploy/payment.wasm

build-all: build-contract build-session build-payment

test: build-contract
	mkdir -p tests/wasm
	cp contract/target/wasm32-unknown-unknown/release/contract.wasm tests/wasm
	cd tests && cargo test

clippy:
	cd contract && cargo clippy --all-targets -- -D warnings

check-lint: clippy
	cd contract && cargo fmt -- --check

lint: clippy
	cd contract && cargo fmt

clean:
	cd contract && cargo clean
	rm -rf tests/wasm

doc:
	cd contract && cargo doc --open