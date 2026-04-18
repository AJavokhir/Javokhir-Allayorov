# Javokhir-Allayorov
Voting DApp
/*
import { useEffect, useState } from "react";
import { ethers } from "ethers";
import "./App.css";

const contractAddress = "0x5FbDB2315678afecb367f032d93F642f64180aa3";

const contractABI = [
  "function vote(uint _candidateId) public",
  "function getCandidate(uint _candidateId) public view returns (uint, string memory, uint)",
  "function candidatesCount() public view returns (uint)"
];

function App() {
  const [account, setAccount] = useState("");
  const [contract, setContract] = useState(null);
  const [candidates, setCandidates] = useState([]);
  const [message, setMessage] = useState("");

  const switchToHardhatNetwork = async () => {
    try {
      await window.ethereum.request({
        method: "wallet_switchEthereumChain",
        params: [{ chainId: "0x7A69" }],
      });
    } catch (switchError) {
      if (switchError.code === 4902) {
        await window.ethereum.request({
          method: "wallet_addEthereumChain",
          params: [
            {
              chainId: "0x7A69",
              chainName: "Hardhat Local",
              rpcUrls: ["http://127.0.0.1:8545"],
              nativeCurrency: {
                name: "ETH",
                symbol: "ETH",
                decimals: 18,
              },
            },
          ],
        });
      } else {
        throw switchError;
      }
    }
  };

  const loadCandidates = async (currentContract) => {
    try {
      const count = Number(await currentContract.candidatesCount());
      const loaded = [];

      for (let i = 1; i <= count; i++) {
        const candidate = await currentContract.getCandidate(i);
        loaded.push({
          id: Number(candidate[0]),
          name: candidate[1],
          voteCount: Number(candidate[2]),
        });
      }

      setCandidates(loaded);
      setMessage("Candidates loaded");
    } catch (error) {
      console.error(error);
      setMessage("Could not load candidates. Check contract address/network.");
    }
  };

  const connectWallet = async () => {
    try {
      if (!window.ethereum) {
        setMessage("MetaMask not found");
        return;
      }

      await switchToHardhatNetwork();
      await window.ethereum.request({ method: "eth_requestAccounts" });

      const provider = new ethers.BrowserProvider(window.ethereum);
      const signer = await provider.getSigner();
      const userAddress = await signer.getAddress();

      const votingContract = new ethers.Contract(contractAddress, contractABI, signer);

      setAccount(userAddress);
      setContract(votingContract);
      setMessage("Wallet connected");

      await loadCandidates(votingContract);
    } catch (error) {
      console.error(error);
      setMessage("Wallet connection failed");
    }
  };

  const vote = async (id) => {
    try {
      if (!contract) {
        setMessage("Connect wallet first");
        return;
      }

      const tx = await contract.vote(id);
      await tx.wait();
      setMessage("Vote submitted successfully");
      await loadCandidates(contract);
    } catch (error) {
      console.error(error);
      setMessage("Voting failed or you already voted");
    }
  };

  useEffect(() => {
    setCandidates([]);
  }, []);

  return (
    <div className="app">
      <h1>Blockchain Voting DApp</h1>

      {!account ? (
        <button onClick={connectWallet}>Connect MetaMask</button>
      ) : (
        <p>Connected: {account}</p>
      )}

      <h2>Candidates</h2>

      {candidates.map((candidate) => (
        <div key={candidate.id} className="card">
          <h3>{candidate.name}</h3>
          <p>Votes: {candidate.voteCount}</p>
          <button onClick={() => vote(candidate.id)}>Vote</button>
        </div>
      ))}

      {message && <p>{message}</p>}
    </div>
  );
}

export default App;
*/
