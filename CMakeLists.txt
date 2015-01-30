if (FIPS_MACOS OR FIPS_WINDOWS OR FIPS_LINUX)

    fips_begin_lib(libuv)

        #include_directories(libuv/include)

        fips_dir(libuv/include)
        fips_files(
            uv.h
            uv-errno.h
            uv-threadpool.h
            uv-version.h
        )

        fips_dir(libuv/src)
        fips_files(
            fs-poll.c
            heap-inl.h
            inet.c
            queue.h
            threadpool.c
            uv-common.c
            uv-common.h
            version.c
        )

        if (FIPS_LINUX OR FIPS_MACOS)
            fips_dir(libuv/include)
            fips_files(
                uv-unix.h
            )

            fips_dir(libuv/src/unix)
            fips_files(
                async.c
                atomic-ops.h
                core.c
                dl.c
                fs.c
                getaddrinfo.c
                getnameinfo.c
                internal.h
                loop-watcher.c
                loop.c
                pipe.c
                poll.c
                process.c
                signal.c
                spinlock.h
                stream.c
                tcp.c
                thread.c
                timer.c
                tty.c
                udp.c
            )
        endif()

        if (FIPS_WINDOWS)
            add_definitions(-DWIN32_LEAN_AND_MEAN)

            fips_dir(libuv/include)
            fips_files(
                uv-win.h
                tree.h
            )

            fips_dir(libuv/src/win)
            fips_files(
                async.c
                atomicops-inl.h
                core.c
                dl.c
                error.c
                fs-event.c
                fs.c
                getaddrinfo.c
                getnameinfo.c
                handle.c
                handle-inl.h
                internal.h
                loop-watcher.c
                pipe.c
                poll.c
                process-stdio.c
                process.c
                req.c
                req-inl.h
                signal.c
                stream.c
                stream-inl.h
                tcp.c
                thread.c
                timer.c
                tty.c
                udp.c
                util.c
                winapi.c
                winapi.h
                winsock.c
                winsock.h
            )
        endif()

    fips_end_lib()

    if(FIPS_WINDOWS)
        set_target_properties(libuv PROPERTIES COMPILE_FLAGS "/wd4054 /wd4100 /wd4127 /wd4201 /wd4204 /wd4210 /wd4242 /wd4244 /wd4245 /wd4389 /wd4668 /wd4996 /wd4701 /wd4702 /wd4703")
    endif()

endif()