import hashlib
import time

class Block:
    def __init__(self, index, timestamp, data, previous_hash=''):
        self.index = index
        self.timestamp = timestamp
        self.data = data
        self.previous_hash = previous_hash
        self.nonce = 0
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        value = str(self.index) + str(self.timestamp) + str(self.data) + str(self.previous_hash) + str(self.nonce)
        return hashlib.sha256(value.encode()).hexdigest()

    def mine_block(self, difficulty):
        target = '0' * difficulty
        while self.hash[:difficulty] != target:
            self.nonce += 1
            self.hash = self.calculate_hash()

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.difficulty = 2

    def create_genesis_block(self):
        return Block(0, time.time(), "Genesis Block", "0")

    def get_latest_block(self):
        return self.chain[-1]

    def add_block(self, data):
        previous_block = self.get_latest_block()
        new_block = Block(len(self.chain), time.time(), data, previous_block.hash)
        new_block.mine_block(self.difficulty)
        self.chain.append(new_block)

    def is_chain_valid(self):
        for i in range(1, len(self.chain)):
            current = self.chain[i]
            previous = self.chain[i - 1]

            if current.hash != current.calculate_hash():
                print(f"❌ Block {i} has invalid hash!")
                return False

            if current.previous_hash != previous.hash:
                print(f"❌ Block {i} has invalid previous hash!")
                return False

        print("✅ Blockchain is valid.")
        return True

    def display_chain(self):
        for block in self.chain:
            print(f"Index: {block.index}")
            print(f"Data: {block.data}")
            print(f"Hash: {block.hash}")
            print(f"Prev Hash: {block.previous_hash}")
            print(f"Nonce: {block.nonce}")
            print("-" * 50)


my_blockchain = Blockchain()
my_blockchain.add_block("Block 1 Data")
my_blockchain.add_block("Block 2 Data")

print("✅ Original Chain:")
my_blockchain.display_chain()
my_blockchain.is_chain_valid()


print("\n⚠️ Tampering Block 1 data...")
my_blockchain.chain[1].data = "Tampered Block 1 Data"
my_blockchain.chain[1].hash = my_blockchain.chain[1].calculate_hash()

print("\n🔎 After Tampering:")
my_blockchain.display_chain()
my_blockchain.is_chain_valid()
