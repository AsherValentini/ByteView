# Advent of Modules — Classic Track
Day 18 Challenge: ByteView

View-only wrapper over raw bytes (std::span-style)

# Goal & Mindset

You’re building a zero-copy, bounds-checked window onto an existing block of memory. Think of it as std::string_view for arbitrary bytes:

- Lightweight (two words: ptr + len)

- Non-owning — lifetime is borrowed

- Cheap to copy — trivially copyable & constexpr friendly

- Safe — no mutation, no overflow, easy slicing

You’ll use this tiny abstraction everywhere: network frames, file-mapped blobs, log lines, var-len protocol fields, etc. Nail the ergonomics now and reap performance later.

```
auto buf = std::array<std::byte, 8>{/* 0x01,0x02,... */};
ByteView view{buf.data(), buf.size()};

auto header  = view.first(2);           // cheap slice
auto payload = view.subview(2);         // remainder

uint16_t id  = header.reinterpret_as<uint16_t_le>(); // stretch-goal API
EXPECT_EQ(payload.size(), 6);

```
