import * as CryptoJS from "crypto-js";

async function cryptoSubtleDigest(algorithm: string, data: Uint8Array): Promise<ArrayBuffer> {
  if (window.crypto?.subtle) {
    return window.crypto.subtle.digest(algorithm, data);
  }

  // Fallback for Safari using CryptoJS
  let hash: CryptoJS.lib.WordArray;
  switch (algorithm.toLowerCase()) {
    case "sha-256":
      hash = CryptoJS.SHA256(CryptoJS.lib.WordArray.create(data));
      break;
    case "sha-1":
      hash = CryptoJS.SHA1(CryptoJS.lib.WordArray.create(data));
      break;
    case "sha-512":
      hash = CryptoJS.SHA512(CryptoJS.lib.WordArray.create(data));
      break;
    default:
      throw new Error(`Unsupported hash algorithm: ${algorithm}`);
  }

  return new Uint8Array(hash.words.flatMap(word => [
    (word >> 24) & 0xff,
    (word >> 16) & 0xff,
    (word >> 8) & 0xff,
    word & 0xff
  ])).buffer;
}

// Override window.crypto.subtle.digest if it's missing
if (!window.crypto?.subtle?.digest) {
  (window.crypto as any).subtle = {
    digest: cryptoSubtleDigest
  };
}
