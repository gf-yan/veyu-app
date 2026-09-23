# Veyu

Cross-language social. You meet people who speak what you are learning, and
private conversations are end-to-end encrypted.

## Why this is open source

The client links [libsignal](https://github.com/signalapp/libsignal), which is
AGPL-3.0, and so is this. That is the licence's doing rather than a marketing
decision — but it is the right outcome anyway. An app whose pitch is that
nobody but the two of you can read a message should be one you can check.

The server is not here, and is not open source. It holds no message keys; what
it can do is hand out the wrong public key, which is what the safety number in
the app is for.

## Encryption, plainly

Direct conversations use the Signal protocol: X3DH with a Kyber1024 prekey, so
key agreement is post-quantum, and the Double Ratchet after that. Keys are
generated on the device and the private halves never leave it.

Group conversations are **not** encrypted, deliberately. Encrypted group
history that survives device loss, admits new members to old messages and can
still be moderated is a set of requirements that do not fit together, and
pretending otherwise would be the dishonest option. The app says which kind of
conversation you are in.

## Layout

    protocol/   the wire format, shared with the server
    lib/        the Flutter client
    ios/        the iOS host project

`protocol/` is the source of truth for the client-to-gateway protocol. The
server repository consumes it as a submodule; the dependency points this way
because a public repository cannot reference a private one.

## Building

Needs the `libsignal_dart` binding, which is a separate AGPL-3.0 package:
<https://github.com/gf-yan/libsignal-dart>.
