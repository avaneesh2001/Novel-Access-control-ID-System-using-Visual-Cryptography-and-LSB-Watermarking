# Visual Cryptography for Biometric Privacy

## Abstract

Biometric data, such as fingerprints, is widely used for authentication systems due to its uniqueness and reliability. However, the security of this sensitive biometric information is a significant concern. In this project, we propose a solution using visual cryptography and LSB watermarking to enhance the security and encryption of fingerprints.

Fingerprint security is crucial as it is commonly employed for convenient and secure authentication, such as on smartphones or in businesses to protect confidential data. Storing fingerprints in a database poses security risks, as a compromise of the database could lead to unauthorized access and potential misuse of the fingerprint data. To address these concerns, encrypted versions of fingerprints are typically stored in the database.

In this project, we propose a visual cryptography scheme (VCS) for encrypting fingerprints. The VCS encrypts each pixel of the original fingerprint image into two subpixels called shares. The choice of shares is randomly determined, ensuring that neither share provides any clue about the original pixel. By separating the shares and storing them in different locations, it becomes challenging to reconstruct the actual fingerprint even if an attacker gains access to one of the shares.

To further enhance security and prevent attackers from detecting hidden information, LSB watermarking is employed. LSB watermarking involves embedding the shares generated by VCS into an innocent cover image. This technique ensures that the hidden information remains concealed, even if an attacker gains access to the database where the shares are stored.

The proposed system addresses the security concerns related to fingerprint authentication by combining visual cryptography and LSB watermarking techniques. By doing so, the system ensures the confidentiality and integrity of fingerprint data, making it challenging for attackers to reconstruct the original fingerprints even if they compromise the database.

## Motivation

The motivation behind this study arises from the need for secure and efficient fingerprint authentication systems in confidential locations, such as restricted areas in companies. Storing fingerprints in a database for authentication purposes presents several challenges, including security concerns and computational power limitations.

The security concern arises from the potential compromise of the fingerprint database, which could lead to unauthorized access and misuse of sensitive information. Unlike passwords, fingerprints cannot be changed, making their security even more critical.

Computational power is another factor to consider, as the decryption process for fingerprints should be feasible on lightweight fingerprint scanners. These devices have limited computational capabilities, and implementing decryption schemes requiring significant resources would be impractical.

To address these challenges, this study aims to develop a system that ensures:

1. Stored fingerprints cannot be effectively decoded, even if the database is compromised.
2. The decryption process can be performed efficiently on lightweight fingerprint scanners without imposing significant computational burdens.

By utilizing visual cryptography and LSB watermarking techniques, this study aims to provide a secure and efficient solution for fingerprint authentication in confidential locations. These techniques enhance the security of stored fingerprints and enable a practical implementation on lightweight fingerprint scanning devices.

The outcomes of this study will contribute to the development of robust biometric privacy mechanisms, ensuring that access to confidential areas is restricted to authorized personnel while maintaining the integrity and security of fingerprint data.

## System Implementation

The proposed system for visual cryptography and fingerprint authentication involves the following steps:

1. **Fingerprint Enrollment**: Authorized personnel have their fingerprints scanned and stored in the company's database. The fingerprints are encrypted using a secure encryption algorithm to protect them from unauthorized access.

2. **Fingerprint Scanner**: At the entrance of the confidential location, a fingerprint scanner is used for authentication. When an employee wants to gain access, they provide their fingerprint for scanning.

3. **Decryption and Watermark Extraction**: Upon scanning the fingerprint, the fingerprint scanner retrieves the corresponding fingerprint share from the company's database. The share is determined based on the employee's ID reduced mod 3, indicating the layer of LSB watermarking performed on the image.

4. **Extraction Algorithm**: The extraction algorithm is used to extract the second share from the layer of the image obtained in the previous step. Both shares are now available for decryption.

5. **Decryption Process**: The shares are decrypted using simple XOR operations, combining the shares to obtain the original fingerprint image. This process ensures that the actual fingerprint cannot be decoded even if the data stored in the database is compromised.

6. **Validation**: To authenticate the employee, the decrypted image matrix is XORed with the scanned fingerprint matrix. The resulting matrix indicates the amount of pixel/bit mismatches. If the mismatch is below a predetermined threshold (e.g., 10%), it is considered a match, and the user is authenticated to access the confidential location.

By incorporating visual cryptography, LSB watermarking, and XOR operations, this system provides a robust approach to fingerprint authentication that enhances security and minimizes computational power requirements. The combination of encryption, decryption, and validation techniques ensures that even if the database is compromised, the original fingerprint cannot be decoded. Additionally, the use of lightweight fingerprint scanners becomes feasible due to the efficient decryption process and threshold-based validation.

## Cryptanalysis
### LSB Watermarking
LSB watermarking provides steganographic security by concealing the encrypted information (VCS share 2) within an innocent cover image (face image). However, it does not offer cryptographic security. For an attacker, the challenge lies in determining which layer of the cover image has been used for LSB watermarking. They would need to attempt extracting the share from all three layers and then decrypt them. It is impossible to discern the actual share from the extracted matrices of zeros and ones, as the share itself appears as random noise. In our implementation, we have utilized the least significant bit (LSB) for watermarking, as it simplifies the extraction process and yields high fidelity with a low peak signal-to-noise ratio (PSNR).

### VCS
Visual Cryptography Scheme (VCS) provides information-theoretic security by employing a visual form of secret sharing. Possessing less than two shares is equivalent to having no shares at all, as the information about one share cannot be derived from the other. Hence, an attacker is left with the daunting task of guessing all possible combinations to obtain the missing share. In our case, the attacker would need to correctly guess one share out of the $2^{300x600}$ possible shares.

Considering that each pixel in the share can be either black or white, there are two possible values for each pixel. Therefore, the attacker needs to guess correctly for all $300 x 600$ pixels, accounting for the expansion in dimensions caused by share generation (twice the original width). When the attacker intercepts the face image during transmission, they must first identify which of the three layers contains the share and then accurately guess the other share.

Furthermore, the attacker would need to determine if a row has been flipped or not. With two possible choices for each row and a total of 600 rows, we have a staggering $3 \times 2^{600} \times 2^{300 \times 600}$ potential options available to the attacker. They must successfully obtain the first share from the cover image, deduce which rows have been flipped, and subsequently determine the other share.

This extensive number of possibilities demonstrates the strength of VCS in protecting the confidentiality of the shares and making it computationally infeasible for an attacker to retrieve the original fingerprint from the intercepted image.

## Conclusion

Visual cryptography and LSB watermarking techniques offer a promising solution for enhancing the security and encryption of fingerprints in biometric authentication systems. By combining these techniques, the proposed system provides robust protection for stored fingerprint data and minimizes the risks associated with database compromises.

The system addresses the challenges of secure fingerprint authentication in confidential locations by leveraging visual cryptography for encryption and LSB watermarking for hiding the encrypted information within innocent cover images. This ensures that unauthorized access to fingerprint data is significantly challenging, even if attackers manage to gain access to the database.

The proposed system also considers the computational limitations of lightweight fingerprint scanners by using efficient decryption algorithms and threshold-based validation techniques. This ensures that the fingerprint authentication process remains practical and feasible on such devices.

Overall, this study contributes to the development of biometric privacy mechanisms, safeguarding sensitive information and ensuring secure access to confidential areas. Future research can explore further improvements and optimizations in visual cryptography and watermarking techniques to enhance the overall security and efficiency of fingerprint authentication systems.