set(wolfssl_VERSION "4.6.0")
set(wolfssl_THIRDPARTY_ROOT "wolfssl-${wolfssl_VERSION}")

file(GLOB WOLF_SRCS
        "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/*.c"
        "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/*.cpp"
        "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/memory.c"
        "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/*.i"
        "${wolfssl_THIRDPARTY_ROOT}/src/*.cpp"
        "${wolfssl_THIRDPARTY_ROOT}/src/*.c"
        "${wolfssl_THIRDPARTY_ROOT}/src/*.s"
)

idf_component_register(
        SRCS
            ${WOLF_SRCS}
        INCLUDE_DIRS
            "."
            "include/"
            "${wolfssl_THIRDPARTY_ROOT}"
        EXCLUDE_SRCS
            "${wolfssl_THIRDPARTY_ROOT}/src/bio.c"
            "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/aes.c"
            "${wolfssl_THIRDPARTY_ROOT}/wolfcrypt/src/aes_asm.s"
        REQUIRES http-parser
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} \
  -DWOLFSSL_USER_SETTINGS \
  -DWOLFCRYPT_HAVE_SRP \
  -DWOLFSSL_SHA512 \
  -DWOLFSSL_BASE64_ENCODE \
 	-DNO_MD5 \
 	-DNO_SHA \
 	-DHAVE_HKDF \
 	-DHAVE_CHACHA \
 	-DHAVE_POLY1305 \
 	-DHAVE_ED25519 \
 	-DHAVE_CURVE25519 \
 	-DNO_SESSION_CACHE \
  -DUSE_WOLFSSL_MEMORY \
 	-DRSA_LOW_MEM \
 	-DGCM_SMALL \
 	-DUSE_SLOW_SHA512 \
 	-DWOLFCRYPT_ONLY \
 	-DCURVE25519_SMALL \
 	-DED25519_SMALL \
  -DESP_IDF"
)