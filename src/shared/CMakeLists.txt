# Copyright (C) 2005-2011 MaNGOS <http://getmangos.com/>
# Copyright (C) 2009-2011 MaNGOSZero <https://github.com/mangos/zero>
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

# Glob only and not recurse, there are other libs for that
set (shared_SRCS
    ByteBuffer.h
    Common.h
    EnumFlag.h
    Errors.h
    Errors.cpp
    LockedQueue.h
    Log.h
    migrations_list.h
    PosixDaemon.h
    ProgressBar.h
    Progression.h
    revision.h
    ServiceWin32.h
    SystemConfig.h
    ThreadPool.h
    ThreadSpecificPtr.h
    ThreadSpecificPtr.cpp
    Timer.h
    Util.h
    WheatyExceptionReport.h
    WorldPacket.h
    Auth/ARC4.h
    Auth/AuthCrypt.h
    Auth/base32.h
    Auth/BigNumber.h
    Auth/Hmac.h
    Auth/HMACSHA1.h
    Auth/md5.h
    Auth/Sha1.h
    Config/Config.h
    Config/ConfigEnv.h
    Database/Database.h
    Database/DatabaseCallback.h
    Database/DatabaseEnv.h
    Database/DatabaseImpl.h
    Database/DatabaseMysql.h
    Database/DatabasePostgre.h
    Database/DBCFileLoader.h
    Database/DBCStore.h
    Database/Field.h
    Database/MySQLDelayThread.h
    Database/PGSQLDelayThread.h
    Database/QueryResult.h
    Database/QueryResultMysql.h
    Database/QueryResultPostgre.h
    Database/SqlDelayThread.h
    Database/SqlOperations.h
    Database/SqlPreparedStatement.h
    Database/SQLStorage.h
    Database/SQLStorageImpl.h
    Multithreading/Messager.h
    SRP6/SRP6.h
    nonstd/expected.hpp
    nonstd/optional.hpp
    ByteBuffer.cpp
    Common.cpp
    Log.cpp
    PosixDaemon.cpp
    ProgressBar.cpp
    ServiceWin32.cpp
    ThreadPool.cpp
    Util.cpp
    Duration.h
    WheatyExceptionReport.cpp
    Auth/ARC4.cpp
    Auth/AuthCrypt.cpp
    Auth/base32.cpp
    Auth/BigNumber.cpp
    Auth/Hmac.cpp
    Auth/HMACSHA1.cpp
    Auth/Sha1.cpp
    Config/Config.cpp
    Database/Database.cpp
    Database/DatabaseMysql.cpp
    Database/DatabasePostgre.cpp
    Database/DBCFileLoader.cpp
    Database/Field.cpp
    Database/QueryResultMysql.cpp
    Database/QueryResultPostgre.cpp
    Database/SqlDelayThread.cpp
    Database/SqlOperations.cpp
    Database/SqlPreparedStatement.cpp
    Database/SQLStorage.cpp
    Multithreading/Messager.cpp
    SRP6/SRP6.cpp
    IO/Context/IoContext.h
    IO/Utils.h
    IO/Utils.cpp
    IO/Utils_Unix.h
    IO/ReadableBuffer.h
    IO/Context/IoContext_macos.cpp
    IO/Context/IoContext_unix.cpp
    IO/Context/IoContext_windows.cpp
    IO/SystemErrorToString.h
    IO/SystemErrorToString.cpp
    IO/Networking/Internal.h
    IO/Networking/Internal.cpp
    IO/Networking/AsyncSocket.h
    IO/Networking/AsyncSocket.cpp
    IO/Networking/AsyncSocket_posix.cpp
    IO/Networking/AsyncSocket_windows.cpp
    IO/Networking/AsyncSocketAcceptor.h
    IO/Networking/AsyncSocketAcceptor_posix.cpp
    IO/Networking/AsyncSocketAcceptor_windows.cpp
    IO/Networking/SocketConnector.h
    IO/Networking/SocketConnector.cpp
    IO/Networking/NetworkError.h
    IO/Networking/NetworkError.cpp
    IO/Networking/SocketDescriptor.h
    IO/Networking/SocketDescriptor.cpp
    IO/Networking/Utils.h
    IO/Networking/Utils.cpp
    IO/Networking/IpAddress.h
    IO/Networking/IpAddress.cpp
    IO/Networking/DNS.h
    IO/Networking/DNS.cpp
    IO/Multithreading/CreateThread.h
    IO/Multithreading/CreateThread.cpp
    IO/Timer/impl/windows/AsyncSystemTimer.cpp
    IO/Timer/impl/windows/TimerHandle.cpp
    IO/Timer/impl/unix/AsyncSystemTimer.cpp
    IO/Timer/impl/unix/TimerHandle.cpp
    IO/Timer/AsyncSystemTimer.h
    IO/Filesystem/FileSystem.h
    IO/Filesystem/FileHandle.h
    IO/Filesystem/impl/windows/FileSystem.cpp
    IO/Filesystem/impl/windows/FileHandle.cpp
    IO/Filesystem/impl/unix/FileSystem.cpp
    IO/Filesystem/impl/unix/FileHandle.cpp
    ProxyProtocol/ProxyV2Reader.h
    ProxyProtocol/ProxyV2Reader.cpp
    ArgparserForServer.h
    ArgparserForServer.cpp
    Memory/ArrayDeleter.h
    Memory/NoDeleter.h
)

if(USE_LIBCURL)
  set (shared_SRCS 
    ${shared_SRCS}
    SendgridMail.h
    MailerService.h
    SendgridMail.cpp
    MailerService.cpp
  )
endif()


if(WIN32) # For window build: Exclude Unix/MacOS files
  list(REMOVE_ITEM shared_SRCS
    PosixDaemon.h
    PosixDaemon.cpp
    revision.h
    migrations_list.h
    IO/Utils_Unix.h
    IO/Context/IoContext_unix.cpp
    IO/Context/IoContext_macos.cpp
    IO/Networking/AsyncSocket_posix.cpp
    IO/Networking/AsyncSocketAcceptor_posix.cpp
    IO/Timer/impl/unix/AsyncSystemTimer.cpp
    IO/Timer/impl/unix/TimerHandle.cpp
    IO/Filesystem/impl/unix/FileSystem.cpp
    IO/Filesystem/impl/unix/FileHandle.cpp
  )
  
  if (NOT MSVC)
    list(REMOVE_ITEM shared_SRCS
      WheatyExceptionReport.cpp
      WheatyExceptionReport.h
    )
  endif()
else()
  list(REMOVE_ITEM shared_SRCS
    WheatyExceptionReport.cpp
    WheatyExceptionReport.h
    ServiceWin32.cpp
    ServiceWin32.h
    revision.h
    migrations_list.h
    IO/Context/IoContext_windows.cpp
    IO/Networking/AsyncSocket_windows.cpp
    IO/Networking/AsyncSocketAcceptor_windows.cpp
    IO/Timer/impl/windows/AsyncSystemTimer.cpp
    IO/Timer/impl/windows/TimerHandle.cpp
    IO/Filesystem/impl/windows/FileSystem.cpp
    IO/Filesystem/impl/windows/FileHandle.cpp
  )
  if(APPLE)
    # Remove Linux specific stuff
    list(REMOVE_ITEM shared_SRCS
      IO/Context/IoContext_unix.cpp
    )
  else()
    # Remove macOS specific stuff
    list(REMOVE_ITEM shared_SRCS
      IO/Context/IoContext_macos.cpp
    )
  endif()
endif()

source_group("Util"
  REGULAR_EXPRESSION .*
)

foreach(SRC ${shared_SRCS})
  get_filename_component(PTH ${SRC} PATH)
  if(PTH)
    if(NOT XCODE) # FIXME: Xcode Generator has bug with nested dirs
      string(REPLACE "/" "\\\\" PTH ${PTH})
    endif()
    source_group(${PTH} FILES ${SRC})
  endif()
endforeach(SRC)

source_group("DataStores"
  REGULAR_EXPRESSION DBC
)

source_group("Log"
  REGULAR_EXPRESSION Log
)

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_SOURCE_DIR}/dep/include
  ${CMAKE_SOURCE_DIR}/src/framework
  ${CMAKE_BINARY_DIR}
  ${MYSQL_INCLUDE_DIR}
  ${OPENSSL_INCLUDE_DIR}
)

if(WIN32)
  include_directories(
    ${CMAKE_SOURCE_DIR}/dep/windows/include
  )
endif()

add_library(shared STATIC
  ${shared_SRCS}
)

if(UNIX)
  find_package(Threads)
  target_link_libraries(shared ${CMAKE_THREAD_LIBS_INIT})
endif(UNIX)

if(WIN32)
  target_link_libraries(shared ws2_32 mswsock)
endif()

target_link_libraries(shared cpptrace::cpptrace)

SET_TARGET_PROPERTIES (shared PROPERTIES FOLDER "Game Libs")
